---
title: "Worklog Tuần 4"
date: 2026-11-23
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Kiểm tra và điều chỉnh lại chi tiết công việc từng ngày cho khớp 100% với lịch cá nhân của bạn nếu cần.
{{% /notice %}}

### Mục tiêu tuần 4 (05/10/2026 – 09/10/2026)

* Làm chủ kiến trúc **Serverless & Event-Driven**: **AWS Lambda**, **Amazon SQS**, và **Dead-Letter Queue (DLQ)**.
* Tìm hiểu dịch vụ cơ sở dữ liệu quản lý **Amazon RDS MySQL** & bảo vệ biên **AWS WAF / CloudFront**.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Nghiên cứu **Amazon SQS**: Standard vs FIFO, Long Polling (`20s`), `VisibilityTimeout` và cấu hình `RedrivePolicy` sang **DLQ**. | 05/10/2026 | 05/10/2026 | <https://docs.aws.amazon.com/sqs/> |
| **3** | - Tìm hiểu **AWS Lambda** (Python 3.12 runtime): Event Source Mapping với SQS, `ReportBatchItemFailures` và `MaximumConcurrency`. | 06/10/2026 | 06/10/2026 | <https://docs.aws.amazon.com/lambda/> |
| **4** | - Thực hành tạo cặp hàng đợi SQS + DLQ và hàm Lambda đọc thông điệp từ SQS qua AWS CLI (`boto3`). | 07/10/2026 | 07/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| **5** | - Tìm hiểu **Amazon RDS MySQL 8.4**: DB Subnet Group trong Private Subnet, Parameter Group TLS và backup/restore tự động. | 08/10/2026 | 08/10/2026 | <https://docs.aws.amazon.com/rds/> |
| **6** | - Tìm hiểu **AWS WAF** (Rate-based rule, Managed Rules) và **Amazon ECR** lưu trữ Docker image bảo mật. | 09/10/2026 | 09/10/2026 | <https://docs.aws.amazon.com/waf/> |

### Kết quả đạt được tuần 4

* Hiểu rõ cách dùng SQS + DLQ để tách biệt luồng xử lý nặng, chống mất job và giới hạn vòng lặp retry lỗi.
* Triển khai thử nghiệm thành công trigger AWS Lambda từ SQS với `BatchSize=1` và cơ chế `ReportBatchItemFailures`.
* Nắm vững mô hình đặt RDS trong Private Subnet chỉ cho phép kết nối từ Security Group của tầng Backend.
