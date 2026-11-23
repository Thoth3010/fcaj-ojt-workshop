---
title: "Workshop: AI Code Judge Pipeline"
date: 2026-11-23
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Building an Asynchronous AI Code Judge Pipeline (Qwen3 / DeepSeek) on AWS

#### Context & Real-World Problem

During hackathons or engineering capstones, judging panels must evaluate dozens or hundreds of GitHub repositories under tight deadlines. Calling an LLM synchronously inside a web API causes `504 Gateway Timeout` failures, running an EC2 GPU (`g4dn.xlarge`) 24/7 costs over `$380/month`, and feeding raw repositories into AI risks secret exposure and prompt injection.

This workshop provides a **100% reproducible, end-to-end guide** to building an **Asynchronous AI Code Judge Pipeline** on **AWS (`ap-southeast-1`)** powered by **7 AWS services**:
1. **Amazon S3 (Private Bucket)** — Immutable artifact store for `inputs/`, `rubrics/`, and idempotent `results/{jobId}/output.json` (`If-None-Match: "*"`).
2. **Amazon SQS + Dead-Letter Queues (DLQs)** — Asynchronous decoupling (`fcaj-ai-jobs-queue` & `fcaj-ai-results-queue`), buffering jobs while EC2 is stopped and isolating poison messages after 3 attempts.
3. **Amazon EC2 (`Ollama + Qwen3`) & AWS Lambda (`Python 3.12`)** — Supports both private VPC Local LLM inference and serverless Lambda execution (`MaximumConcurrency = 2`).
4. **AWS IAM (Least Privilege)** — Scoped execution permissions restricted to specific S3 prefixes and queue ARNs.
5. **AWS Systems Manager (SSM Parameter Store)** — KMS-encrypted `SecureString` storage for API tokens, eliminating hardcoded secrets.
6. **Amazon CloudWatch (Logs, Metrics & Alarms)** — Real-time execution logs, queue metrics, and DLQ failure alarms.
7. **Amazon SNS & AWS Budgets** — Instant email alerting for DLQ anomalies and spending thresholds.

---

#### Alignment with the AWS Well-Architected Framework (6 Pillars)

| Pillar | Implementation in This Workshop |
| :--- | :--- |
| **Operational Excellence** | Scripted provisioning (`aws` CLI + `setup_ec2_ollama.sh`), centralized CloudWatch logging, and automated unit/contract tests (`13/13 PASS`). |
| **Security** | Prefix-scoped IAM Least Privilege; S3 Block Public Access; SSM `SecureString`; `<CANDIDATE_SOURCE_CODE>` prompt isolation; automated `redact_secrets`. |
| **Reliability** | SQS + DLQ (`maxReceiveCount = 3`), background SQS heartbeat, SHA-256 verification, and conditional idempotent S3 writes (`If-None-Match: "*"`). |
| **Performance Efficiency** | `OLLAMA_FLASH_ATTENTION=1`, `OLLAMA_KV_CACHE_TYPE=q8_0` (50% VRAM savings), `/no_think` fast mode (-65% latency), and Smart Repo Slicing. |
| **Cost Optimization** | SQS buffering allows stopping GPU EC2 when idle (`$0/hr`), EC2 Spot (`~$0.16–$0.20/hr`), Lambda Free Tier, and full clean-up to `$0.00`. |
| **Sustainability** | Compute activates strictly on demand; `code_cleaner.py` strips lockfiles/binaries to minimize wasted tokens and energy. |

---

#### Workshop Outline

1. **[5.1. Architecture Overview & Data Flow](5.1-workshop-overview/)**
2. **[5.2. Prerequisites & Cost Estimation (AWS Pricing Calculator)](5.2-prerequiste/)**
3. **[5.3. Provisioning S3, SQS/DLQ, SSM & IAM Least Privilege](5.3-s3-sqs-iam/)**
4. **[5.4. Deploying the AI Judge Worker (EC2 Qwen3 & AWS Lambda)](5.4-deploy-ai-worker/)**
5. **[5.5. Testing, CloudWatch Monitoring, Live Demo & Troubleshooting](5.5-testing-monitoring/)**
6. **[5.6. Complete Resource Clean-up](5.6-cleanup/)**
