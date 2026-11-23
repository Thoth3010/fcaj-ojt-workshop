---
title: "Nhật ký công việc (Worklog)"
date: 2026-11-23
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Lịch trình 12 tuần (`14/09/2026 – 14/12/2026`) dưới đây đã được lập sẵn theo chuẩn Daily Worklog (Thứ 2 → Thứ 6 mỗi tuần, kèm ngày bắt đầu/hoàn thành và tài liệu tham khảo AWS chính thống) dựa trên quá trình học AWS và phát triển module **AI Judge (`ai-worker/`)** của dự án **SEAL Hackathon**. Bạn hãy kiểm tra và điều chỉnh lại chi tiết theo lịch làm việc thực tế của mình nếu cần nhé!
{{% /notice %}}

### Tổng quan Nhật ký Thực tập 12 Tuần (`14/09/2026 – 14/12/2026`)

1. **[Tuần 1 (14/09 – 18/09/2026)](1.1-week1/):** Định hướng FCAJ, thiết lập AWS Account an toàn (MFA, AWS Budgets), AWS CLI & Tổng quan AWS Cloud.
2. **[Tuần 2 (21/09 – 25/09/2026)](1.2-week2/):** Mạng ảo AWS (Amazon VPC, Subnets, Route Tables, IGW/NAT, Security Groups) & Amazon EC2.
3. **[Tuần 3 (28/09 – 02/10/2026)](1.3-week3/):** Bảo mật danh tính (AWS IAM Roles, Policies, Least Privilege) & Lưu trữ (Amazon S3, Block Public Access, Lifecycle).
4. **[Tuần 4 (05/10 – 09/10/2026)](1.4-week4/):** Serverless, Hàng đợi & Cơ sở dữ liệu (AWS Lambda, Amazon SQS/DLQ, Amazon RDS MySQL, CloudFront & WAF).
5. **[Tuần 5 (12/10 – 16/10/2026)](1.5-week5/):** Giám sát hệ thống (CloudWatch Logs/Metrics/Alarms, SNS, SSM Parameter Store) & Khởi động đề tài SEAL Hackathon.
6. **[Tuần 6 (19/10 – 23/10/2026)](1.6-week6/):** Thiết kế kiến trúc AWS cho SEAL Hackathon, chốt Tech Stack & JSON Contracts (`fcaj.ai.message.v1`).
7. **[Tuần 7 (26/10 – 30/10/2026)](1.7-week7/):** Phát triển `code_cleaner.py`, `schema.py`, `mock_worker.py` và rà soát đồng bộ Input/Output Schema.
8. **[Tuần 8 (02/11 – 06/11/2026)](1.8-week8/):** Phát triển `ai_grader.py`, tích hợp Cloud AI (`DeepSeek` / `Gemini`), bảo mật chống Prompt Injection & kiểm thử tự động (`10/10` -> `13/13` tests).
9. **[Tuần 9 (09/11 – 13/11/2026)](1.9-week9/):** Chuyển đổi & Benchmark Local AI (`Ollama` + `Qwen3`) trên AWS EC2 (`ap-southeast-1`), tối ưu `KV Cache q8_0` & Smart Repo Slicing.
10. **[Tuần 10 (16/11 – 20/11/2026)](1.10-week10/):** Xây dựng `lambda_handler.py` & `sqs_worker.py` chuẩn contract v3, kiểm thử SHA-256, `If-None-Match: "*"` & SQS Heartbeat.
11. **[Tuần 11 (23/11 – 27/11/2026)](1.11-week11/):** Tích hợp giám sát CloudWatch Alarms/SNS, tính toán AWS Pricing Calculator, viết 3 Blogs & hoàn thiện Workshop song ngữ.
12. **[Tuần 12 (30/11 – 04/12/2026)](1.12-week12/):** Diễn tập Live Demo E2E, hoàn tất báo cáo cuối khóa, dọn dẹp triệt để tài nguyên AWS (`$0.00`) & chuẩn bị nghiệm thu OJT.
