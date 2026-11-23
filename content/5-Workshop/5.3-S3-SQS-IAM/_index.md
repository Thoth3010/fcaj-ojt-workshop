---
title: "Provision S3, SQS/DLQ, SSM & IAM Least Privilege"
date: 2026-11-23
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

In this lab step, we provision the private storage bucket, asynchronous queues with Dead-Letter Queues, encrypted parameter store, and a **Least Privilege IAM Role** in `ap-southeast-1`.

### Step 1: Set Environment Variables

```bash
export AWS_REGION="ap-southeast-1"
export ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)
export BUCKET_NAME="fcaj-ai-judge-data-${ACCOUNT_ID}-ap-southeast-1"
echo "Account: $ACCOUNT_ID | Bucket: $BUCKET_NAME"
```

---

### Step 2: Create a Private Amazon S3 Bucket (Block Public Access & Lifecycle)

```bash
# 1. Create the S3 Bucket in ap-southeast-1
aws s3api create-bucket \
  --bucket "$BUCKET_NAME" \
  --region "$AWS_REGION" \
  --create-bucket-configuration LocationConstraint="$AWS_REGION"

# 2. Enforce Block All Public Access (Security Pillar)
aws s3api put-public-access-block \
  --bucket "$BUCKET_NAME" \
  --public-access-block-configuration \
    "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true"

# 3. Add a Lifecycle Rule to expire temporary inputs after 30 days (Cost Optimization)
aws s3api put-bucket-lifecycle-configuration \
  --bucket "$BUCKET_NAME" \
  --lifecycle-configuration '{
    "Rules": [{
      "ID": "ExpireTempInputsAfter30Days",
      "Filter": { "Prefix": "poc/inputs/" },
      "Status": "Enabled",
      "Expiration": { "Days": 30 }
    }]
  }'
```

---

### Step 3: Provision 4 Amazon SQS Queues (Jobs/Results + DLQs)

```bash
# 1. Create Dead-Letter Queues (DLQs)
aws sqs create-queue --queue-name fcaj-ai-jobs-dlq --region "$AWS_REGION"
aws sqs create-queue --queue-name fcaj-ai-results-dlq --region "$AWS_REGION"

export JOBS_DLQ_URL=$(aws sqs get-queue-url --queue-name fcaj-ai-jobs-dlq --query QueueUrl --output text)
export JOBS_DLQ_ARN=$(aws sqs get-queue-attributes --queue-url "$JOBS_DLQ_URL" --attribute-names QueueArn --query Attributes.QueueArn --output text)

export RESULTS_DLQ_URL=$(aws sqs get-queue-url --queue-name fcaj-ai-results-dlq --query QueueUrl --output text)
export RESULTS_DLQ_ARN=$(aws sqs get-queue-attributes --queue-url "$RESULTS_DLQ_URL" --attribute-names QueueArn --query Attributes.QueueArn --output text)

# 2. Create Jobs Queue with RedrivePolicy (maxReceiveCount = 3) & VisibilityTimeout = 720s
aws sqs create-queue \
  --queue-name fcaj-ai-jobs-queue \
  --region "$AWS_REGION" \
  --attributes "{
    \"VisibilityTimeout\": \"720\",
    \"ReceiveMessageWaitTimeSeconds\": \"20\",
    \"RedrivePolicy\": \"{\\\"deadLetterTargetArn\\\":\\\"${JOBS_DLQ_ARN}\\\",\\\"maxReceiveCount\\\":\\\"3\\\"}\"
  }"

# 3. Create Results Queue with RedrivePolicy
aws sqs create-queue \
  --queue-name fcaj-ai-results-queue \
  --region "$AWS_REGION" \
  --attributes "{
    \"VisibilityTimeout\": \"120\",
    \"ReceiveMessageWaitTimeSeconds\": \"20\",
    \"RedrivePolicy\": \"{\\\"deadLetterTargetArn\\\":\\\"${RESULTS_DLQ_ARN}\\\",\\\"maxReceiveCount\\\":\\\"3\\\"}\"
  }"
```

---

### Step 4: Store API Credentials in SSM Parameter Store (`SecureString`)

Never commit API keys to Git or pass plaintext credentials in source files:

```bash
aws ssm put-parameter \
  --name "/fcaj/poc/deepseek-api-key" \
  --type "SecureString" \
  --value "<YOUR_DEEPSEEK_OR_DEMO_API_KEY>" \
  --region "$AWS_REGION"
```

---

### Step 5: Create the Least Privilege IAM Role & Inline Policy

Create `trust-policy.json` allowing AWS Lambda (and EC2 if using Option A) to assume the role:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": { "Service": ["lambda.amazonaws.com", "ec2.amazonaws.com"] },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

Create `ai-worker-least-privilege.json` scoping access strictly to exact S3 prefixes and queue ARNs:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ReadInputsAndRubricsOnly",
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:GetObjectVersion"],
      "Resource": [
        "arn:aws:s3:::fcaj-ai-judge-data-<ACCOUNT_ID>-ap-southeast-1/poc/inputs/*",
        "arn:aws:s3:::fcaj-ai-judge-data-<ACCOUNT_ID>-ap-southeast-1/poc/rubrics/*"
      ]
    },
    {
      "Sid": "WriteResultsOnly",
      "Effect": "Allow",
      "Action": ["s3:PutObject", "s3:GetObject"],
      "Resource": "arn:aws:s3:::fcaj-ai-judge-data-<ACCOUNT_ID>-ap-southeast-1/poc/results/*"
    },
    {
      "Sid": "ConsumeJobsQueue",
      "Effect": "Allow",
      "Action": [
        "sqs:ReceiveMessage",
        "sqs:DeleteMessage",
        "sqs:ChangeMessageVisibility",
        "sqs:GetQueueAttributes"
      ],
      "Resource": "arn:aws:sqs:ap-southeast-1:<ACCOUNT_ID>:fcaj-ai-jobs-queue"
    },
    {
      "Sid": "PublishResultsQueue",
      "Effect": "Allow",
      "Action": "sqs:SendMessage",
      "Resource": "arn:aws:sqs:ap-southeast-1:<ACCOUNT_ID>:fcaj-ai-results-queue"
    },
    {
      "Sid": "ReadScopedSSMParameter",
      "Effect": "Allow",
      "Action": "ssm:GetParameter",
      "Resource": "arn:aws:ssm:ap-southeast-1:<ACCOUNT_ID>:parameter/fcaj/poc/deepseek-api-key"
    }
  ]
}
```

Apply the IAM Role and attach `AWSLambdaBasicExecutionRole` for CloudWatch logging:

```bash
sed "s/<ACCOUNT_ID>/${ACCOUNT_ID}/g" ai-worker-least-privilege.json > policy-resolved.json

aws iam create-role \
  --role-name fcaj-ai-worker-role \
  --assume-role-policy-document file://trust-policy.json

aws iam attach-role-policy \
  --role-name fcaj-ai-worker-role \
  --policy-arn arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole

aws iam put-role-policy \
  --role-name fcaj-ai-worker-role \
  --policy-name fcaj-ai-worker-least-privilege \
  --policy-document file://policy-resolved.json
```
