---
title: "Kiểm thử, CloudWatch Monitoring & Demo"
date: 2026-11-23
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

### 1. Kiểm thử Tự động (Unit, Contract & Security Tests)

Chạy toàn bộ bộ kiểm thử tự động trong thư mục `ai-worker/`:

```bash
cd ai-worker
python -m unittest discover -s tests -v
```

**Kết quả kiểm chứng thực tế đã ghi nhận:**
- **13/13 Unit & Integration Tests (`test_ai_worker.py`) PASS 100% trong `0.032s`**:
  - Kiểm chứng tự động làm sạch tiền tố số dòng (`strip_line_number_prefix`).
  - Kiểm chứng tự động che mật khẩu / API Key (`redact_secrets` -> `***REDACTED***`).
  - Kiểm chứng tính lại điểm trung bình trọng số chính xác (`compute_weighted_overall_score`).
  - Kiểm chứng phát hiện cắt cụt output (`finish_reason == "length"`).
  - Kiểm chứng contract `fcaj.ai.message.v1`, SHA-256 mismatch và hành vi idempotent khi S3 trả về `PreconditionFailed`.

---

### 2. Kiểm thử Luồng End-to-End (E2E) & Kịch bản Lỗi (Fault Injection)

#### A. Đẩy job mẫu lên S3 & SQS (Happy Path)
```bash
# Upload sample source & rubric lên S3 và gửi message kiểm thử vào fcaj-ai-jobs-queue
aws s3 cp contracts/sample_input.json "s3://${BUCKET_NAME}/poc/inputs/demo-job-01/source.json"

aws sqs send-message \
  --queue-url "$APP_AI_JOBS_JOBS_QUEUE_URL" \
  --region "$AWS_REGION" \
  --message-body '{"schemaVersion":"fcaj.ai.message.v1","messageType":"AI_JOB_REQUESTED","jobId":"demo-job-01",...}'

# Kiểm tra kết quả sau 20-30 giây trên S3 và Results Queue
aws s3 ls "s3://${BUCKET_NAME}/poc/results/demo-job-01/"
aws sqs receive-message --queue-url "$APP_AI_JOBS_RESULTS_QUEUE_URL" --wait-time-seconds 10
```

#### B. Kiểm thử Kịch bản Lỗi (Poison Message -> DLQ)
Gửi một message JSON sai định dạng (thiếu trường bắt buộc hoặc sai SHA-256) vào `fcaj-ai-jobs-queue`:
```bash
aws sqs send-message \
  --queue-url "$APP_AI_JOBS_JOBS_QUEUE_URL" \
  --message-body '{"invalid":"payload-test-dlq"}'
```
- Worker ném lỗi `ContractValidationError` -> SQS giữ lại và tự thử lại đúng 3 lần (`maxReceiveCount = 3`), sau đó tự động đẩy message sang **`fcaj-ai-jobs-dlq`** và kích hoạt CloudWatch Alarm.

---

### 3. Thiết lập Giám sát CloudWatch Logs, Metrics, Alarms & SNS

Tạo SNS Topic gửi email cảnh báo khi có bất kỳ job nào rơi vào Dead-Letter Queue hoặc Lambda gặp lỗi:

```bash
# 1. Tạo SNS Topic và đăng ký Email nhận cảnh báo (nhớ mở hòm thư bấm Confirm Subscription)
export ALERT_TOPIC_ARN=$(aws sns create-topic --name fcaj-ai-alerts --region "$AWS_REGION" --query TopicArn --output text)
aws sns subscribe \
  --topic-arn "$ALERT_TOPIC_ARN" \
  --protocol email \
  --notification-endpoint "trieuquan3010@gmail.com" \
  --region "$AWS_REGION"

# 2. Tạo CloudWatch Alarm cảnh báo ngay khi có message rơi vào Jobs DLQ (> 0)
aws cloudwatch put-metric-alarm \
  --alarm-name "FCAJ-AI-Jobs-DLQ-NotEmpty" \
  --alarm-description "Alert when any AI grading job enters Dead-Letter Queue" \
  --namespace "AWS/SQS" \
  --metric-name "ApproximateNumberOfMessagesVisible" \
  --dimensions Name=QueueName,Value=fcaj-ai-jobs-dlq \
  --statistic Sum \
  --period 60 \
  --evaluation-periods 1 \
  --threshold 0 \
  --comparison-operator GreaterThanThreshold \
  --alarm-actions "$ALERT_TOPIC_ARN" \
  --region "$AWS_REGION"

# 3. Tạo CloudWatch Alarm cảnh báo lỗi Lambda Worker
aws cloudwatch put-metric-alarm \
  --alarm-name "FCAJ-AI-Lambda-Errors" \
  --namespace "AWS/Lambda" \
  --metric-name "Errors" \
  --dimensions Name=FunctionName,Value=fcaj-ai-judge-worker \
  --statistic Sum \
  --period 60 \
  --evaluation-periods 1 \
  --threshold 1 \
  --comparison-operator GreaterThanOrEqualToThreshold \
  --alarm-actions "$ALERT_TOPIC_ARN" \
  --region "$AWS_REGION"
```

Kiểm tra log thực tế của Lambda qua AWS CLI:
```bash
aws logs tail /aws/lambda/fcaj-ai-judge-worker --since 15m --follow --region "$AWS_REGION"
```

---

### 4. Số liệu Benchmark Thực tế trên AWS (`ap-southeast-1`)

| Môi trường / Mô hình kiểm thử | Quy mô Repo / Model | Thời gian xử lý | Độ chuẩn JSON Schema | Ghi chú chi phí |
| :--- | :--- | :---: | :---: | :--- |
| **EC2 `t3.small` (Free Tier, 2 vCPU + 4GB Swap)** | `qwen3:0.6b` (`Ollama`, `/no_think`, `q8_0`) | `50.77s` | **100% PASS** | **`$0.00`** (Terminate sau test) |
| **Cloud AI Fallback (`DeepSeek-V4.1-Flash` / `V3`)** | Repo thật `lead-hackathon-test` (`49 files`, `7,257 dòng`, `~117k tokens`) | **`19.71s`** | **100% PASS** | **`~$0.0175 / job`** (`$0.0045` nếu Cache Hit) |
| **EC2 GPU Spot dự kiến (`g4dn.xlarge` — 16GB T4)** | `Qwen3-14B` (`Q4_K_M`, `16k context`) | `~15s – 28s` | **100% PASS** | `~$0.18/giờ` Spot (`$3.2–$4.0/tháng`) |

---

### 5. Minh chứng Sản phẩm Chạy Thực tế (Live Demo / Video)

{{% notice warning %}}
🎬 **`[TODO - Viết lại sau — BẮT BUỘC TRƯỚC KHI NỘP]`:** Theo quy định FCAJ, không có minh chứng sản phẩm chạy thực tế sẽ nhận **0 điểm mục Demo**. Hãy chèn link Video Demo (YouTube / Google Drive quay màn hình luồng gửi SQS -> Worker xử lý -> xem kết quả trên S3 & CloudWatch Logs) hoặc link Production Live Demo tại đây:

- **Link Video Demo (Unlisted YouTube / Google Drive):** `[TODO - Viết lại sau: Dán link video quay màn hình demo thực tế tại đây]`
- **Link Source Code Repository:** `[TODO - Viết lại sau: Link GitHub repo của hệ thống nếu public]`
{{% /notice %}}

---

### 6. Đóng góp Cá nhân & Xử lý Sự cố (Troubleshooting & Reflection)

Trong quá trình tự nghiên cứu và triển khai module `ai-worker/`, mình đã trực tiếp phát hiện và giải quyết 4 thách thức kỹ thuật cốt lõi:

1. **Tràn VRAM khi repo vượt quá 90k tokens (`OOM`):**
   - *Giải pháp:* Kích hoạt `OLLAMA_KV_CACHE_TYPE=q8_0` + `OLLAMA_FLASH_ATTENTION=1` (giảm 50% VRAM) và viết thuật toán **Smart Repo Slicing** trong `code_cleaner.py` ưu tiên file nguồn chính mà vẫn giữ nguyên số thứ tự dòng gốc.
2. **LLM tính nhầm điểm trung bình trọng số (`7.55` vs `7.45`):**
   - *Giải pháp:* Tách hẳn phép tính điểm tổng ra khỏi LLM; Python tự tính lại `overall_score` từ điểm thành phần và trọng số `rubrics[].weight`.
3. **Nguy cơ lộ Credentials từ code thí sinh trong Evidence & Prompt Injection:**
   - *Giải pháp:* Bọc code trong `<CANDIDATE_SOURCE_CODE>` và viết lớp lọc regex `redact_secrets()` che toàn bộ API key, password thành `***REDACTED***`.
4. **SQS phát lại tin nhắn khi Local AI chạy lâu vượt `VisibilityTimeout`:**
   - *Giải pháp:* Bổ sung luồng nền Heartbeat gọi `change_message_visibility()` mỗi 45 giây và khóa ghi S3 idempotent bằng `IfNoneMatch="*"`.
