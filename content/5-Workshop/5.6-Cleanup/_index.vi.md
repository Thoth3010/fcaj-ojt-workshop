---
title: "Dọn dẹp tài nguyên (Clean-up)"
date: 2026-11-23
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

{{% notice warning %}}
⚠️ **Bắt buộc sau khi hoàn thành Workshop:** Chạy đầy đủ các bước dưới đây để xóa sạch toàn bộ tài nguyên đã tạo tại Region `ap-southeast-1`, đảm bảo không phát sinh chi phí ngoài ý muốn trên tài khoản AWS của bạn (`$0.00`).
{{% /notice %}}

### Thứ tự Dọn dẹp Tài nguyên Chuẩn (AWS CLI)

#### 1. Xóa Event Source Mapping & AWS Lambda Function (nếu dùng Option B)
```bash
export AWS_REGION="ap-southeast-1"

# Liệt kê và xóa Event Source Mapping
for uuid in $(aws lambda list-event-source-mappings --function-name fcaj-ai-judge-worker --region "$AWS_REGION" --query 'EventSourceMappings[].UUID' --output text); do
  aws lambda delete-event-source-mapping --uuid "$uuid" --region "$AWS_REGION"
done

# Xóa Lambda Function
aws lambda delete-function --function-name fcaj-ai-judge-worker --region "$AWS_REGION"
```

#### 2. Tắt (Terminate) EC2 Instance & Xóa EBS / Security Group / KeyPair (nếu dùng Option A)
```bash
# Thay <INSTANCE_ID> và <SG_ID> bằng ID máy ảo thử nghiệm của bạn
aws ec2 terminate-instances --instance-ids <INSTANCE_ID> --region "$AWS_REGION"
aws ec2 wait instance-terminated --instance-ids <INSTANCE_ID> --region "$AWS_REGION"
aws ec2 delete-security-group --group-id <SG_ID> --region "$AWS_REGION"
```

#### 3. Xóa 4 Hàng đợi Amazon SQS (Jobs, Jobs DLQ, Results, Results DLQ)
```bash
for q in fcaj-ai-jobs-queue fcaj-ai-jobs-dlq fcaj-ai-results-queue fcaj-ai-results-dlq; do
  Q_URL=$(aws sqs get-queue-url --queue-name "$q" --region "$AWS_REGION" --query QueueUrl --output text 2>/dev/null || true)
  if [ -n "$Q_URL" ]; then
    aws sqs delete-queue --queue-url "$Q_URL" --region "$AWS_REGION"
    echo "Deleted SQS: $q"
  fi
done
```

#### 4. Làm rỗng (Empty) và Xóa Amazon S3 Bucket
*(Amazon S3 không cho phép xóa bucket khi vẫn còn object bên trong)*
```bash
export ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)
export BUCKET_NAME="fcaj-ai-judge-data-${ACCOUNT_ID}-ap-southeast-1"

aws s3 rm "s3://${BUCKET_NAME}" --recursive --region "$AWS_REGION"
aws s3api delete-bucket --bucket "$BUCKET_NAME" --region "$AWS_REGION"
```

#### 5. Xóa SSM Parameter, CloudWatch Alarms, Log Groups & SNS Topic
```bash
# Xóa SSM Parameter
aws ssm delete-parameter --name "/fcaj/poc/deepseek-api-key" --region "$AWS_REGION"

# Xóa CloudWatch Alarms & Log Group
aws cloudwatch delete-alarms --alarm-names "FCAJ-AI-Jobs-DLQ-NotEmpty" "FCAJ-AI-Lambda-Errors" --region "$AWS_REGION"
aws logs delete-log-group --log-group-name "/aws/lambda/fcaj-ai-judge-worker" --region "$AWS_REGION"

# Xóa SNS Topic
ALERT_TOPIC_ARN=$(aws sns list-topics --region "$AWS_REGION" --query "Topics[?ends_with(TopicArn, ':fcaj-ai-alerts')].TopicArn" --output text)
if [ -n "$ALERT_TOPIC_ARN" ]; then
  aws sns delete-topic --topic-arn "$ALERT_TOPIC_ARN" --region "$AWS_REGION"
fi
```

#### 6. Gỡ Inline Policy & Xóa IAM Role
```bash
aws iam delete-role-policy --role-name fcaj-ai-worker-role --policy-name fcaj-ai-worker-least-privilege
aws iam detach-role-policy --role-name fcaj-ai-worker-role --policy-arn arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole
aws iam delete-role --role-name fcaj-ai-worker-role
```

---

### Checklist Kiểm tra Sau Dọn dẹp (`$0.00` Verification)

- [ ] **EC2 Dashboard (`ap-southeast-1`):** `0` Running instances, `0` Available EBS Volumes, `0` Elastic IPs chưa giải phóng.
- [ ] **AWS Lambda & SQS:** Không còn function `fcaj-ai-judge-worker` và 4 queues `fcaj-ai-*`.
- [ ] **Amazon S3:** Bucket `fcaj-ai-judge-data-*` đã bị xóa hoàn toàn.
- [ ] **AWS Billing & Cost Management:** Kiểm tra **Bills** và **Free Tier Usage** sau 24 giờ để xác nhận không còn chi phí phát sinh thêm.
