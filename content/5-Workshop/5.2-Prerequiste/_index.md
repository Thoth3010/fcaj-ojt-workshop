---
title: "Prerequisites & Cost Estimation"
date: 2026-11-23
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

### 1. Prerequisites

Before starting the hands-on steps, ensure you have:

- **AWS Account:** Recommended region **`ap-southeast-1` (Singapore)** for low latency in Vietnam, with Root MFA enabled and **AWS Budgets** alerts configured (`$1` / `$5`).
- **IAM Permissions:** An IAM User/Role permitted to manage S3 buckets, SQS queues, SSM parameters, IAM execution roles, Lambda/EC2, and CloudWatch Alarms.
- **Local Tooling:**
  - **AWS CLI v2** (authenticated via `aws login` or `aws configure`)
  - **Python 3.12+** and **Git**
  - **Reference AI Worker Source:** `ai-worker/` (`src/`, `scripts/`, `tests/`).

Quick environment verification:
```bash
aws --version
aws sts get-caller-identity --region ap-southeast-1
python --version
```

---

### 2. Detailed Cost Estimation (AWS Pricing Calculator — `ap-southeast-1`)

{{% notice warning %}}
💰 **Mandatory Cost Section:** The figures below are modeled using the **AWS Pricing Calculator** in `ap-southeast-1` for a realistic workload of **200 AI grading jobs per month** (one 50-team hackathon round).
{{% /notice %}}

#### Scenario 1: Serverless Workshop Mode (Option B — AWS Lambda + S3 + SQS + CloudWatch)

| AWS Service | Configuration | Monthly Volume | Unit Rate | Est. Monthly Cost |
| :--- | :--- | :--- | :--- | :---: |
| **Amazon S3** | Private Standard Bucket (Block Public Access) | `1 GB` stored, `2,000 PUT`, `4,000 GET` | `$0.025/GB` (5 GB Free Tier Year 1) | **$0.03** |
| **Amazon SQS** | 4 Standard Queues (`Jobs`, `Jobs-DLQ`, `Results`, `Results-DLQ`) | `~10,000 requests` | `$0.40 / 1M req` (Always Free `1M` req) | **$0.00** |
| **AWS Lambda** | Python 3.12, `512 MB RAM`, avg `20s/job` | `200 invocations` (`2,000 GB-s`) | Always Free `400,000 GB-s` & `1M` req | **$0.00** |
| **SSM Parameter Store** | 1 Standard `SecureString` Parameter | `< 10,000 API calls` | Standard tier is free | **$0.00** |
| **CloudWatch & SNS** | Log Group (14-day retention), `2 Alarms`, Email SNS | `< 1 GB` logs, `2` alarms | Free Tier `5 GB` logs & `10` alarms | **$0.00** |
| **Cloud AI API (DeepSeek)** | `deepseek-chat` (`~117k in / 4k out tokens` per job) | `200 jobs` (Off-peak `$0.02/job`) | `$0.15/1M in`, `$0.60/1M out` | **~$3.50 – $4.00** |
| **TOTAL (Serverless)** | | | | **~$3.53 – $4.03 / month** |

#### Scenario 2: Private Local LLM Mode on AWS EC2 (Option A — Zero External Source Transfer)

| EC2 Configuration (`ap-southeast-1`) | Monthly Active Hours | Compute Cost | EBS `30 GB gp3` | Est. Monthly Total |
| :--- | :--- | :---: | :---: | :---: |
| **Free Tier Smoke Test (`t3.small` / `m7i-flex.large`)** | 2-hour lab test then `Terminate` | `$0.00` (Free Tier) | `$0.00` | **$0.00** |
| **Production GPU Spot (`g4dn.xlarge` — 1x T4 16GB VRAM)** | Active during judging windows: **`20 hrs/mo`** (`~$0.18/hr` Spot) | `$3.60` | `$2.88` | **~$6.48 / month** |
| **Comparison: 24/7 On-Demand (`g4dn.xlarge`)** | `730 hrs/mo` (`$0.526/hr`) | `$383.98` | `$2.88` | **$386.86 / month** |

---

### 3. Cost Optimization Best Practices Applied

1. **SQS-Buffered On-Demand GPU Execution (-98.4% Compute Spend):** Because SQS safely retains jobs for up to 14 days, the GPU EC2 stays `Stopped` (`$0/hr`) whenever no hackathon judging window is active.
2. **EC2 Fail-Safe Auto-Shutdown:** `setup_ec2_ollama.sh` schedules `shutdown -h +45` to prevent accidental overnight GPU billing.
3. **`q8_0` KV-Cache & `/no_think` Mode:** Fits `Qwen3-14B` cleanly within a 16GB T4 (`g4dn.xlarge`) instead of a 2x more expensive `g5.xlarge`, while slashing per-job duration by 65%.
4. **S3 Lifecycle & Short Log Retention:** Expire temporary source snapshots after 30 days and cap CloudWatch Log retention at 7–14 days.
5. **AWS Free Tier & Concurrency Caps:** Lambda `MaximumConcurrency = 2` keeps usage safely inside Free Tier limits and caps third-party API bursts.
