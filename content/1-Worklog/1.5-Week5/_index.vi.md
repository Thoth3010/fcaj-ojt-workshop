---
title: "Worklog Tuần 5"
date: 2026-11-23
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Kiểm tra và điều chỉnh lại chi tiết công việc từng ngày cho khớp 100% với lịch cá nhân của bạn nếu cần.
{{% /notice %}}

### Mục tiêu tuần 5 (12/10/2026 – 16/10/2026)

* Làm chủ bộ công cụ giám sát và quản lý bí mật: **Amazon CloudWatch**, **Amazon SNS** và **SSM Parameter Store**.
* Nghiên cứu yêu cầu nghiệp vụ dự án **SEAL / FCAJ Hackathon System** và nhận phân công vai trò **AI Engineer**.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Nghiên cứu **Amazon CloudWatch**: Log Groups, Log Insights, Custom Metrics và thiết lập CloudWatch Alarms. | 12/10/2026 | 12/10/2026 | <https://docs.aws.amazon.com/cloudwatch/> |
| **3** | - Thực hành tạo **Amazon SNS Topic**, đăng ký email alert và gắn vào CloudWatch Alarm cảnh báo queue DLQ (`> 0`). | 13/10/2026 | 13/10/2026 | <https://docs.aws.amazon.com/sns/> |
| **4** | - Thực hành lưu secret `SecureString` trên **AWS Systems Manager Parameter Store** và cấp quyền đọc KMS/SSM cho IAM Role. | 14/10/2026 | 14/10/2026 | <https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html> |
| **5** | - Họp nhóm khởi động dự án **SEAL Hackathon System**, đọc tài liệu SRS, Use Case và quy trình chấm điểm. | 15/10/2026 | 15/10/2026 | `docs/documents/ProjectRequirements.md` |
| **6** | - Phân tích bài toán **AI Judge Assistant**: xác định yêu cầu chấm code theo Rubric kèm bằng chứng (file, dòng code) cho giám khảo. | 16/10/2026 | 16/10/2026 | <https://docs.aws.amazon.com/wellarchitected/> |

### Kết quả đạt được tuần 5

* Thiết lập được luồng cảnh báo tự động từ CloudWatch Alarms gửi qua Amazon SNS về email vận hành.
* Biết cách loại bỏ hoàn toàn API key khỏi source code nhờ SSM Parameter Store `SecureString`.
* Nắm rõ yêu cầu nghiệp vụ và phạm vi kỹ thuật của module `ai-worker/` trong dự án SEAL Hackathon.
