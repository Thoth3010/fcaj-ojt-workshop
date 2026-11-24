---
title: "Nhật ký công việc (Worklog)"
date: 2026-11-23
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Nhật ký 12 tuần (`14/09/2026 – 14/12/2026`) dưới đây đã phân bổ lộ trình 295+ video thuộc khóa học chính thức **First Cloud Journey (`PLahN4TLWtox2a3vElknwzU_urND8hLn1i`)** kết hợp cùng tiến độ thực chiến xây dựng dự án **SEAL Hackathon Platform & AI Judge (`ai-worker/`)** của nhóm. Bạn hãy kiểm tra và điều chỉnh lại lịch chi tiết nếu cần nhé!
{{% /notice %}}

### Tổng quan Nhật ký Thực tập 12 Tuần (`14/09/2026 – 14/12/2026`)

1. **[Tuần 1 (14/09 – 18/09/2026)](1.1-week1/):** Kick-off First Cloud Journey & **Module 01** (Cloud Foundations, Tạo AWS Account, Virtual MFA, Admin Group/User, AWS Budgets & Support).
2. **[Tuần 2 (21/09 – 25/09/2026)](1.2-week2/):** **Module 02 (Phần 1)** — Amazon VPC, Subnets, Route Table, IGW/NAT, Security Group, NACL, EC2 Instance Connect Endpoint & Hybrid DNS Route 53 Resolver.
3. **[Tuần 3 (28/09 – 02/10/2026)](1.3-week3/):** **Module 02 (Phần 2) & Module 03 (Phần 1)** — VPC Peering, Transit Gateway, EC2 Instance Types/AMI/EBS/UserData/Auto Scaling & AWS Backup (`Lab 13`).
4. **[Tuần 4 (05/10 – 09/10/2026)](1.4-week4/):** **Module 03 (Phần 2) & Module 04 (Phần 1)** — Storage Gateway (`Lab 24`), S3 Static Website + CloudFront + Versioning + Multi-Region Replication (`Lab 57`), S3 Storage Classes & VM Import/Export (`Lab 14`).
5. **[Tuần 5 (12/10 – 16/10/2026)](1.5-week5/):** **Module 04 (Phần 2) & Module 05 (Phần 1)** — Amazon FSx (`Lab 25`), Shared Responsibility, IAM, Cognito, KMS, Security Hub (`Lab 18`), Lambda Auto Start/Stop EC2 (`Lab 22`) & **Khởi động dự án SEAL Hackathon**.
6. **[Tuần 6 (19/10 – 23/10/2026)](1.6-week6/):** **Module 05 (Phần 2 — IAM Chuyên sâu, CloudTrail & Athena)** (`Lab 27, 28, 30, 33, 44, 48`) + **Thiết kế Kiến trúc AWS & Contracts (`fcaj.ai.message.v1`) cho SEAL Hackathon**.
7. **[Tuần 7 (26/10 – 30/10/2026)](1.7-week7/):** **Module 06 — Databases** (RDS, Aurora, Redshift, ElastiCache, `Lab 05` VPC+EC2+RDS, `Lab 43` AWS DMS) + **Phát triển `schema.py`, `code_cleaner.py` & `mock_worker.py`**.
8. **[Tuần 8 (02/11 – 06/11/2026)](1.8-week8/):** **Module 07 (Phần 1 — DynamoDB, Event-Driven LEDA & SDK)** (`Lab 39, 40, 60`) + **Phát triển `ai_grader.py`, `redact_secrets()`, Benchmark Cloud AI (`19.71s`) & Unit Tests**.
9. **[Tuần 9 (09/11 – 13/11/2026)](1.9-week9/):** **Module 07 (Phần 2 — Data Pipeline, Glue, Athena, QuickSight & Lambda Serving)** (`Lab 35, 70, 72, 73`) + **Triển khai & Benchmark Local AI (`Ollama + Qwen3`) trên AWS EC2 (`ap-southeast-1`)**.
10. **[Tuần 10 (16/11 – 20/11/2026)](1.10-week10/):** **Áp dụng Serverless + IAM Role (`Lab 22, Lab 48, Lab 39`) vào Kiến trúc AWS v3 của Dự án SEAL** — Xây dựng `lambda_handler.py`, `sqs_worker.py`, kiểm tra SHA-256 & S3 Idempotency (`If-None-Match: "*"`).
11. **[Tuần 11 (23/11 – 27/11/2026)](1.11-week11/):** **Thực hành theo video `Hướng dẫn vẽ kiến trúc AWS trên draw.io` & `Hướng dẫn làm workshop AWS`** — Thiết lập CloudWatch Alarms/SNS, tính AWS Pricing Calculator, viết 3 Blogs & dựng Workshop song ngữ VI/EN.
