---
title: "Khởi tạo S3, SQS/DLQ, SSM & IAM Least Privilege"
date: 2026-11-23
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

Trong bước thực hành này, chúng ta sẽ khởi tạo hạ tầng lưu trữ, hàng đợi, quản lý bí mật và phân quyền IAM chuẩn **Least Privilege** tại vùng `ap-southeast-1`.

### Bước 1: Thiết lập biến môi trường làm việc

```bash
export AWS_REGION="ap-southeast-1"
export ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)
export BUCKET_NAME="fcaj-ai-judge-data-${ACCOUNT_ID}-ap-southeast-1"
echo "Account: $ACCOUNT_ID | Bucket: $BUCKET_NAME"
```

---

### Bước 2: Tạo Amazon S3 Private Bucket (Chặn Public Access & Bật Mã hóa)

```bash
# 1. Tạo S3 Bucket tại Singapore (ap-southeast-1)
aws s3api create-bucket \
  --bucket "$BUCKET_NAME" \
  --region "$AWS_REGION" \
  --create-bucket-configuration LocationConstraint="$AWS_REGION"

# 2. Bắt buộc bật Block All Public Access (Security Pillar)
aws s3api put-public-access-block \
  --bucket "$BUCKET_NAME" \
  --public-access-block-configuration \
    "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true"

# 3. Thiết lập Lifecycle tự động xóa snapshot đầu vào tạm sau 30 ngày (Cost Optimization)
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

### Bước 3: Tạo 4 hàng đợi Amazon SQS (Jobs/Results + Dead-Letter Queues)

```bash
# 1. Tạo 2 Dead-Letter Queues (DLQs)
aws sqs create-queue --queue-name fcaj-ai-jobs-dlq --region "$AWS_REGION"
aws sqs create-queue --queue-name fcaj-ai-results-dlq --region "$AWS_REGION"

export JOBS_DLQ_URL=$(aws sqs get-queue-url --queue-name fcaj-ai-jobs-dlq --query QueueUrl --output text)
export JOBS_DLQ_ARN=$(aws sqs get-queue-attributes --queue-url "$JOBS_DLQ_URL" --attribute-names QueueArn --query Attributes.QueueArn --output text)

export RESULTS_DLQ_URL=$(aws sqs get-queue-url --queue-name fcaj-ai-results-dlq --query QueueUrl --output text)
export RESULTS_DLQ_ARN=$(aws sqs get-queue-attributes --queue-url "$RESULTS_DLQ_URL" --attribute-names QueueArn --query Attributes.QueueArn --output text)

# 2. Tạo Jobs Queue gắn RedrivePolicy (maxReceiveCount = 3) & VisibilityTimeout = 720s (an toàn cho Lambda 120s)
aws sqs create-queue \
  --queue-name fcaj-ai-jobs-queue \
  --region "$AWS_REGION" \
  --attributes "{
    \"VisibilityTimeout\": \"720\",
    \"ReceiveMessageWaitTimeSeconds\": \"20\",
    \"RedrivePolicy\": \"{\\\"deadLetterTargetArn\\\":\\\"${JOBS_DLQ_ARN}\\\",\\\"maxReceiveCount\\\":\\\"3\\\"}\"
  }"

# 3. Tạo Results Queue gắn RedrivePolicy
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

### Bước 4: Lưu API Key vào SSM Parameter Store (`SecureString`)

Tuyệt đối không lưu API Key dưới dạng plaintext trong code hoặc GitHub:

```bash
aws ssm put-parameter \
  --name "/fcaj/poc/deepseek-api-key" \
  --type "SecureString" \
  --value "<YOUR_DEEPSEEK_OR_DEMO_API_KEY>" \
  --region "$AWS_REGION"
```

---

### Bước 5: Tạo IAM Role & Policy tuân thủ Nguyên tắc Least Privilege

Tạo file `trust-policy.json` cho phép AWS Lambda (hoặc EC2) đảm nhận vai trò:

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

Tạo file `ai-worker-least-privilege.json` chỉ cấp đúng quyền cần thiết theo từng prefix S3 và queue ARN cụ thể:

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

Áp dụng IAM Role và gắn chính sách cơ bản để đẩy log lên CloudWatch:

```bash
# Thay thế <ACCOUNT_ID> bằng Account ID thật trước khi chạy
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
