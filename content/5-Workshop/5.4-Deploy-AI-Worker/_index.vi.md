---
title: "Triển khai AI Judge Worker (EC2 Qwen3 & Lambda)"
date: 2026-11-23
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

Hệ thống AI Judge hỗ trợ linh hoạt hai phương án triển khai sử dụng chung lõi bảo mật và xử lý dữ liệu (`code_cleaner.py`, `ai_grader.py`, `schema.py`):

---

### Lựa chọn A: Triển khai Local LLM (`Ollama + Qwen3`) trên AWS EC2

Phù hợp khi cần **bảo mật tuyệt đối 100% mã nguồn trong VPC AWS**, không gửi code ra API bên thứ ba.

#### 1. Cài đặt tự động Ollama & tối ưu VRAM (`setup_ec2_ollama.sh`)
Khi khởi tạo EC2 Ubuntu 24.04 (`g4dn.xlarge` Spot hoặc `m7i-flex.large` / `t3.small` khi test Free Tier), truyền script sau vào **UserData**:

```bash
#!/bin/bash
set -euxo pipefail

MODEL_NAME="${1:-qwen3:4b}"
AUTO_SHUTDOWN_MINUTES="${2:-45}"

# 1. Chốt chặn an toàn: Tự động tắt máy sau 45 phút chống phát sinh chi phí nếu quên tắt
if [ "$AUTO_SHUTDOWN_MINUTES" -gt 0 ]; then
  shutdown -h +"$AUTO_SHUTDOWN_MINUTES" "FCAJ fail-safe auto-shutdown" || true
fi

# 2. Tạo 4GB Swap trên ổ NVMe gp3 chống tràn RAM cho máy Free Tier
if [ ! -f /swapfile ]; then
  fallocate -l 4G /swapfile && chmod 600 /swapfile
  mkswap /swapfile && swapon /swapfile
  echo '/swapfile none swap sw 0 0' >> /etc/fstab
fi

# 3. Cài đặt Ollama & bật Flash Attention + KV Cache q8_0 (giảm 50% VRAM/RAM)
export DEBIAN_FRONTEND=noninteractive
apt-get update -y && apt-get install -y curl zstd jq
curl -fsSL https://ollama.com/install.sh | sh

mkdir -p /etc/systemd/system/ollama.service.d
cat << 'EOF' > /etc/systemd/system/ollama.service.d/override.conf
[Service]
Environment="OLLAMA_HOST=127.0.0.1:11434"
Environment="OLLAMA_FLASH_ATTENTION=1"
Environment="OLLAMA_KV_CACHE_TYPE=q8_0"
Environment="OLLAMA_KEEP_ALIVE=-1"
Environment="OLLAMA_NUM_PARALLEL=1"
EOF

systemctl daemon-reload && systemctl enable ollama && systemctl restart ollama
sleep 5
ollama pull "$MODEL_NAME"
```

#### 2. Các cơ chế bảo vệ & tối ưu lõi AI (`code_cleaner.py` & `ai_grader.py`)
- **Smart Repo Slicing (`code_cleaner.py`):** Ưu tiên thu thập file trong `src/`, `app/`, `back-end/`, `front-end/` đúng ngôn ngữ mục tiêu (`_file_priority_key`), loại bỏ thư mục rác (`node_modules`, `target`, `.git`), lockfile (`package-lock.json`) và tự động đánh số thứ tự dòng gốc để AI trích dẫn `line_start` – `line_end` chính xác.
- **Chế độ `/no_think` & Hậu kiểm (`ai_grader.py`):**
  - Chèn `/no_think` giúp Qwen3 bỏ qua nháp dài dòng, giảm **~65% thời gian chờ** (hoặc dùng regex lọc thẻ `<think>...</think>`).
  - Bọc mã nguồn thí sinh trong thẻ `<CANDIDATE_SOURCE_CODE>...</CANDIDATE_SOURCE_CODE>` để chống **Prompt Injection**.
  - Tự động che secret (`redact_secrets()`) thành `***REDACTED***` và tính lại điểm tổng kết bằng Python (`compute_weighted_overall_score()`).

Chạy SQS Worker trên EC2 (tự động long-polling 20 giây & gia hạn `VisibilityTimeout`):
```bash
export AI_PROVIDER="local_ai"
export LOCAL_AI_BASE_URL="http://127.0.0.1:11434/v1/chat/completions"
export LOCAL_AI_MODEL="qwen3:14b"
export APP_STORAGE_BUCKET="$BUCKET_NAME"
export APP_STORAGE_PREFIX="poc"
export APP_AI_JOBS_JOBS_QUEUE_URL=$(aws sqs get-queue-url --queue-name fcaj-ai-jobs-queue --query QueueUrl --output text)
export APP_AI_JOBS_RESULTS_QUEUE_URL=$(aws sqs get-queue-url --queue-name fcaj-ai-results-queue --query QueueUrl --output text)

python src/sqs_worker.py
```

---

### Lựa chọn B: Triển khai Serverless trên AWS Lambda (`Python 3.12`)

Phù hợp cho bài lab Serverless không tốn chi phí chờ (`$0` khi nhàn rỗi). Hàm `lambda_handler.py` nằm **ngoài VPC** (không cần NAT Gateway và không có quyền truy cập RDS).

#### 1. Đóng gói và tạo AWS Lambda Function

```bash
cd ai-worker
zip -r lambda-ai-worker.zip src/

export WORKER_ROLE_ARN=$(aws iam get-role --role-name fcaj-ai-worker-role --query Role.Arn --output text)
export JOBS_QUEUE_ARN=$(aws sqs get-queue-attributes --queue-url "$APP_AI_JOBS_JOBS_QUEUE_URL" --attribute-names QueueArn --query Attributes.QueueArn --output text)

aws lambda create-function \
  --function-name fcaj-ai-judge-worker \
  --runtime python3.12 \
  --handler src.lambda_handler.lambda_handler \
  --role "$WORKER_ROLE_ARN" \
  --zip-file fileb://lambda-ai-worker.zip \
  --timeout 120 \
  --memory-size 512 \
  --region "$AWS_REGION" \
  --environment "Variables={
    AI_PROVIDER=deepseek,
    DEEPSEEK_MODEL=deepseek-chat,
    DEEPSEEK_API_KEY_PARAMETER=/fcaj/poc/deepseek-api-key,
    APP_STORAGE_BUCKET=$BUCKET_NAME,
    APP_STORAGE_PREFIX=poc,
    APP_AI_JOBS_RESULTS_QUEUE_URL=$APP_AI_JOBS_RESULTS_QUEUE_URL,
    LAMBDA_MAX_SOURCE_CHARS=120000
  }"
```

#### 2. Gắn Trigger SQS (`BatchSize = 1` & `MaximumConcurrency = 2`)

```bash
aws lambda create-event-source-mapping \
  --function-name fcaj-ai-judge-worker \
  --event-source-arn "$JOBS_QUEUE_ARN" \
  --batch-size 1 \
  --function-response-types "ReportBatchItemFailures" \
  --scaling-config "MaximumConcurrency=2" \
  --region "$AWS_REGION"
```

{{% notice tip %}}
✅ **Điểm thiết kế quan trọng trong `lambda_handler.py`:**
1. **Xác thực SHA-256 & Byte Size:** Kiểm tra khớp checksum của `input-manifest.json`, `source.json`, `rubric.json` trước khi chấm.
2. **Idempotent S3 Write:** Ghi kết quả lên `poc/results/{jobId}/output.json` với `IfNoneMatch="*"` đảm bảo SQS retry không bao giờ ghi đè sai kết quả đã hoàn tất.
3. **Cache Warm-Start SSM:** API key đọc từ `/fcaj/poc/deepseek-api-key` được giữ ở biến module để tái sử dụng qua các lần gọi warm của Lambda.
{{% /notice %}}
