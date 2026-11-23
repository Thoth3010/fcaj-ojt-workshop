---
title: "Worklog Tuần 3"
date: 2026-11-23
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Kiểm tra và điều chỉnh lại chi tiết công việc từng ngày cho khớp 100% với lịch cá nhân của bạn nếu cần.
{{% /notice %}}

### Mục tiêu tuần 3 (28/09/2026 – 02/10/2026)

* Thực hành quản trị danh tính & phân quyền **AWS IAM** theo nguyên tắc **Least Privilege** (quyền tối thiểu).
* Làm chủ **Amazon S3**: Bucket Policy, Block Public Access, mã hóa SSE-S3, Lifecycle Policy & S3 Gateway Endpoint.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Nghiên cứu cấu trúc JSON **IAM Policy**, phân biệt Identity-based vs Resource-based Policy, IAM Role & Trust Policy (`AssumeRole`). | 28/09/2026 | 28/09/2026 | <https://docs.aws.amazon.com/iam/> |
| **3** | - Thực hành viết IAM Policy giới hạn quyền theo Resource ARN và prefix cụ thể (chặn `AdministratorAccess` cho workload). | 29/09/2026 | 29/09/2026 | <https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html> |
| **4** | - Nghiên cứu **Amazon S3**: Storage Classes, Versioning, Block Public Access và điều kiện ghi idempotent (`If-None-Match: "*"`). | 30/09/2026 | 30/09/2026 | <https://docs.aws.amazon.com/s3/> |
| **5** | - Thực hành tạo Private S3 Bucket, bật Block Public Access, thiết lập S3 Lifecycle xóa file tạm sau 30 ngày để tối ưu chi phí. | 01/10/2026 | 01/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| **6** | - Tìm hiểu kết nối **S3 Gateway Endpoint** trong VPC và thực hành **CloudFront Origin Access Control (OAC)** cho static website. | 02/10/2026 | 02/10/2026 | <https://docs.aws.amazon.com/AmazonCloudFront/> |

### Kết quả đạt được tuần 3

* Thành thạo thiết kế IAM Role và Inline Policy tuân thủ Least Privilege theo từng prefix trên S3.
* Biết cách bảo mật S3 bucket hoàn toàn riêng tư (Block Public Access) và tối ưu chi phí lưu trữ bằng Lifecycle Rule.
* Hiểu cơ chế CloudFront OAC và S3 Gateway Endpoint giúp giảm chi phí băng thông mạng nội bộ.
