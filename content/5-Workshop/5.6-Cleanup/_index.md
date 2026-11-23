---
title: "Resource Clean-up"
date: 2026-11-23
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

{{% notice warning %}}
⚠️ **Mandatory Post-Lab Step:** Execute every step below to completely tear down all workshop resources in `ap-southeast-1` and guarantee `$0.00` ongoing AWS charges.
{{% /notice %}}

### Clean-up Sequence (AWS CLI)

#### 1. Remove Event Source Mapping & AWS Lambda Function (Option B)
```bash
export AWS_REGION="ap-southeast-1"

for uuid in $(aws lambda list-event-source-mappings --function-name fcaj-ai-judge-worker --region "$AWS_REGION" --query 'EventSourceMappings[].UUID' --output text); do
  aws lambda delete-event-source-mapping --uuid "$uuid" --region "$AWS_REGION"
done

aws lambda delete-function --function-name fcaj-ai-judge-worker --region "$AWS_REGION"
```

#### 2. Terminate EC2 Instance & Remove Security Group / EBS (Option A)
```bash
# Replace <INSTANCE_ID> and <SG_ID> with your test IDs
aws ec2 terminate-instances --instance-ids <INSTANCE_ID> --region "$AWS_REGION"
aws ec2 wait instance-terminated --instance-ids <INSTANCE_ID> --region "$AWS_REGION"
aws ec2 delete-security-group --group-id <SG_ID> --region "$AWS_REGION"
```

#### 3. Delete All 4 Amazon SQS Queues (Jobs, Jobs DLQ, Results, Results DLQ)
```bash
for q in fcaj-ai-jobs-queue fcaj-ai-jobs-dlq fcaj-ai-results-queue fcaj-ai-results-dlq; do
  Q_URL=$(aws sqs get-queue-url --queue-name "$q" --region "$AWS_REGION" --query QueueUrl --output text 2>/dev/null || true)
  if [ -n "$Q_URL" ]; then
    aws sqs delete-queue --queue-url "$Q_URL" --region "$AWS_REGION"
    echo "Deleted SQS: $q"
  fi
done
```

#### 4. Empty and Delete the Amazon S3 Bucket
*(S3 buckets must be empty before deletion)*
```bash
export ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)
export BUCKET_NAME="fcaj-ai-judge-data-${ACCOUNT_ID}-ap-southeast-1"

aws s3 rm "s3://${BUCKET_NAME}" --recursive --region "$AWS_REGION"
aws s3api delete-bucket --bucket "$BUCKET_NAME" --region "$AWS_REGION"
```

#### 5. Delete SSM Parameter, CloudWatch Alarms, Log Groups & SNS Topic
```bash
aws ssm delete-parameter --name "/fcaj/poc/deepseek-api-key" --region "$AWS_REGION"

aws cloudwatch delete-alarms --alarm-names "FCAJ-AI-Jobs-DLQ-NotEmpty" "FCAJ-AI-Lambda-Errors" --region "$AWS_REGION"
aws logs delete-log-group --log-group-name "/aws/lambda/fcaj-ai-judge-worker" --region "$AWS_REGION"

ALERT_TOPIC_ARN=$(aws sns list-topics --region "$AWS_REGION" --query "Topics[?ends_with(TopicArn, ':fcaj-ai-alerts')].TopicArn" --output text)
if [ -n "$ALERT_TOPIC_ARN" ]; then
  aws sns delete-topic --topic-arn "$ALERT_TOPIC_ARN" --region "$AWS_REGION"
fi
```

#### 6. Remove Inline Policy & Delete IAM Role
```bash
aws iam delete-role-policy --role-name fcaj-ai-worker-role --policy-name fcaj-ai-worker-least-privilege
aws iam detach-role-policy --role-name fcaj-ai-worker-role --policy-arn arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole
aws iam delete-role --role-name fcaj-ai-worker-role
```

---

### Post-Cleanup Verification Checklist (`$0.00` Audit)

- [ ] **EC2 Console (`ap-southeast-1`):** `0` running instances, `0` unattached EBS volumes, `0` unallocated Elastic IPs.
- [ ] **AWS Lambda & SQS:** Confirm `fcaj-ai-judge-worker` and all four `fcaj-ai-*` queues are deleted.
- [ ] **Amazon S3:** Confirm `fcaj-ai-judge-data-*` bucket no longer exists.
- [ ] **AWS Billing & Cost Management:** Re-check **Bills** and **Free Tier Usage** after 24 hours to confirm zero recurring spend.
