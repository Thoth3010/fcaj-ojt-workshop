---
title: "Deploy the AI Judge Worker (EC2 Qwen3 & Lambda)"
date: 2026-11-23
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

The AI Judge architecture supports two interchangeable deployment modes sharing the same sanitized ingestion and post-processing core (`code_cleaner.py`, `ai_grader.py`, `schema.py`):

---

### Option A: Private Local LLM (`Ollama + Qwen3`) on AWS EC2

Best suited when **100% of candidate source code must remain strictly inside your AWS VPC** without third-party API calls.

#### 1. Automated Ollama Setup & Memory Tuning (`setup_ec2_ollama.sh`)
Pass this script as EC2 **UserData** on Ubuntu 24.04 (`g4dn.xlarge` Spot for production or `m7i-flex.large` / `t3.small` for Free Tier smoke testing):

```bash
#!/bin/bash
set -euxo pipefail

MODEL_NAME="${1:-qwen3:4b}"
AUTO_SHUTDOWN_MINUTES="${2:-45}"

# 1. Fail-safe guardrail: Auto-shutdown after 45 minutes if forgotten
if [ "$AUTO_SHUTDOWN_MINUTES" -gt 0 ]; then
  shutdown -h +"$AUTO_SHUTDOWN_MINUTES" "FCAJ fail-safe auto-shutdown" || true
fi

# 2. Allocate 4GB NVMe gp3 Swap for Free Tier RAM protection
if [ ! -f /swapfile ]; then
  fallocate -l 4G /swapfile && chmod 600 /swapfile
  mkswap /swapfile && swapon /swapfile
  echo '/swapfile none swap sw 0 0' >> /etc/fstab
fi

# 3. Install Ollama + enable Flash Attention & q8_0 KV Cache (50% VRAM reduction)
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

#### 2. Core AI Safeguards & Optimizations (`code_cleaner.py` & `ai_grader.py`)
- **Smart Repo Slicing (`code_cleaner.py`):** Prioritizes core directories (`src/`, `app/`, `back-end/`, `front-end/`) via `_file_priority_key`, excludes dependency/build noise (`node_modules`, `target`, `.git`, lockfiles), and tags every line with its original source line number.
- **Fast `/no_think` Mode & Post-Processing (`ai_grader.py`):**
  - Appends `/no_think` so Qwen3 skips verbose reasoning chains (cutting latency by **~65%**) and strips any residual `<think>...</think>` blocks.
  - Wraps repository contents inside `<CANDIDATE_SOURCE_CODE>...</CANDIDATE_SOURCE_CODE>` to defend against **Prompt Injection**.
  - Runs regex `redact_secrets()` (`***REDACTED***`) and deterministic Python weighted averaging (`compute_weighted_overall_score()`).

Start the long-polling SQS worker on EC2:
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

### Option B: Serverless Execution on AWS Lambda (`Python 3.12`)

Ideal for zero-idle-cost serverless operation. `lambda_handler.py` runs **outside the VPC** (no NAT Gateway charges and zero network access to RDS).

#### 1. Package & Create the AWS Lambda Function

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

#### 2. Attach SQS Trigger (`BatchSize = 1` & `MaximumConcurrency = 2`)

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
✅ **Key Reliability & Security Details in `lambda_handler.py`:**
1. **SHA-256 & Byte-Size Verification:** Validates `input-manifest.json`, `source.json`, and `rubric.json` checksums before running inference.
2. **Idempotent S3 Write:** Uses conditional PutObject (`IfNoneMatch="*"`) on `poc/results/{jobId}/output.json` so SQS retries never overwrite completed outputs.
3. **Warm-Start SSM Caching:** Fetches `/fcaj/poc/deepseek-api-key` once per execution environment and caches it across warm invocations.
{{% /notice %}}
