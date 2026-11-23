---
title: "Workshop: AI Code Judge Pipeline"
date: 2026-11-23
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Xây dựng Hệ thống Chấm Code Tự Động Bất Đồng Bộ với AI Judge (Qwen3 / DeepSeek) trên AWS

#### Bối cảnh & Bài toán thực tế

Trong các kỳ thi Hackathon hoặc đánh giá đồ án kỹ thuật, hội đồng giám khảo phải kiểm tra hàng chục đến hàng trăm repository GitHub trong thời gian ngắn. Việc gọi LLM đồng bộ trực tiếp trong luồng HTTP gây nghẽn (`504 Gateway Timeout`), trong khi bật máy chủ GPU (`EC2 g4dn.xlarge`) 24/7 lại tốn hơn `$380/tháng` và dễ phát sinh rủi ro lộ mã nguồn hoặc bí mật (secrets) nếu thiếu lớp kiểm soát bảo mật.

Workshop này hướng dẫn **từng bước từ đầu đến cuối (End-to-End Reproducible)** cách xây dựng **Hệ thống Chấm Code Tự Động Bất Đồng Bộ (Asynchronous AI Code Judge Pipeline)** trên **AWS (`ap-southeast-1`)** sử dụng **7 dịch vụ AWS**:
1. **Amazon S3 (Private Bucket)** — Lưu trữ bất biến `inputs/`, `rubrics/` và kết quả `results/{jobId}/output.json` (ghi idempotent với `If-None-Match: "*"`).
2. **Amazon SQS + Dead-Letter Queues (DLQs)** — Tách luồng bất đồng bộ (`fcaj-ai-jobs-queue` & `fcaj-ai-results-queue`), giữ job khi EC2 tắt và cô lập message lỗi sau 3 lần thử.
3. **Amazon EC2 (Local LLM `Ollama + Qwen3`) & AWS Lambda (`Python 3.12`)** — Hỗ trợ song song cả chạy Local AI riêng tư trong VPC lẫn Serverless Lambda (`MaximumConcurrency = 2`) gọi Cloud AI fallback.
4. **AWS IAM (Least Privilege)** — Phân quyền chặt chẽ theo từng prefix S3 và ARN hàng đợi SQS cụ thể.
5. **AWS Systems Manager (SSM Parameter Store)** — Lưu API Key dưới dạng `SecureString` mã hóa KMS, loại bỏ 100% hard-code secret.
6. **Amazon CloudWatch (Logs, Metrics & Alarms)** — Giám sát nhật ký worker, độ sâu hàng đợi và phát hiện lỗi DLQ tức thì.
7. **Amazon SNS & AWS Budgets** — Gửi email cảnh báo ngay khi có job lỗi vào DLQ hoặc chi phí vượt ngưỡng.

---

#### Tuân thủ AWS Well-Architected Framework (6 Pillars)

| Pillar | Cách Workshop hiện thực hóa |
| :--- | :--- |
| **Operational Excellence** | Triển khai tự động bằng AWS CLI & script Bash (`setup_ec2_ollama.sh`), log tập trung trên CloudWatch và kiểm thử tự động (`13/13` unit/contract tests). |
| **Security** | IAM Least Privilege theo ARN/prefix; S3 Block Public Access; SSM `SecureString`; chống Prompt Injection (`<CANDIDATE_SOURCE_CODE>`); tự động che secret (`redact_secrets`). |
| **Reliability** | Kiến trúc hướng sự kiện SQS + DLQ (`maxReceiveCount = 3`), gia hạn `VisibilityTimeout` bằng Heartbeat, kiểm tra SHA-256 và ghi S3 idempotent (`If-None-Match: "*"`). |
| **Performance Efficiency** | Tối ưu suy luận Qwen3 bằng `OLLAMA_FLASH_ATTENTION=1`, `OLLAMA_KV_CACHE_TYPE=q8_0` (giảm 50% VRAM), chế độ `/no_think` (giảm 65% latency) và Smart Repo Slicing. |
| **Cost Optimization** | SQS giữ job cho phép tắt EC2 GPU khi nhàn rỗi (`$0/giờ`), sử dụng EC2 Spot (`~$0.16–$0.20/giờ`), Lambda Free Tier và dọn dẹp sạch tài nguyên về `$0.00`. |
| **Sustainability** | Chỉ khởi chạy compute AI đúng thời điểm có job trong hàng đợi, tối ưu lượng token truyền vào LLM thông qua `code_cleaner.py`. |

---

#### Nội dung chi tiết của Workshop

1. **[5.1. Tổng quan Kiến trúc & Luồng dữ liệu](5.1-workshop-overview/)**
2. **[5.2. Điều kiện tiên quyết & Dự toán chi phí (Cost Estimation)](5.2-prerequiste/)**
3. **[5.3. Khởi tạo S3, SQS/DLQ, SSM & IAM Least Privilege](5.3-s3-sqs-iam/)**
4. **[5.4. Triển khai AI Judge Worker (EC2 Qwen3 & AWS Lambda)](5.4-deploy-ai-worker/)**
5. **[5.5. Kiểm thử, CloudWatch Monitoring, Demo & Troubleshooting](5.5-testing-monitoring/)**
6. **[5.6. Dọn dẹp tài nguyên triệt để (Clean-up)](5.6-cleanup/)**
