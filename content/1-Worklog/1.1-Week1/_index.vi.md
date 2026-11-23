---
title: "Worklog Tuần 1"
date: 2026-11-23
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Kiểm tra và điều chỉnh lại chi tiết công việc từng ngày cho khớp 100% với lịch cá nhân của bạn nếu cần.
{{% /notice %}}

### Mục tiêu tuần 1 (14/09/2026 – 18/09/2026)

* Làm quen văn hóa làm việc, quy định nộp bài OJT và đồng đội trong **First Cloud AI Journey (FCAJ)**.
* Thiết lập tài khoản AWS Free Tier an toàn (bật MFA, thiết lập **AWS Budgets** cảnh báo chi phí).
* Cài đặt và làm chủ giao diện **AWS Management Console** cùng **AWS CLI v2**.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Tham gia buổi định hướng đầu kỳ FCAJ.<br>- Đọc kỹ quy định thực tập, tiêu chí đánh giá OJT & cấu trúc báo cáo song ngữ.<br>- Kết nối với mentor và thành viên nhóm. | 14/09/2026 | 14/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| **3** | - Tìm hiểu kiến trúc tổng quan AWS Global Infrastructure (Regions, Availability Zones).<br>- Phân loại các nhóm dịch vụ cốt lõi: Compute, Storage, Networking, Database, Security. | 15/09/2026 | 15/09/2026 | <https://docs.aws.amazon.com/> |
| **4** | - Khởi tạo AWS Free Tier Account.<br>- Bật MFA cho tài khoản Root & tạo IAM Admin User thay thế.<br>- Cấu hình **AWS Budgets** ($1 & $5 threshold alert). | 16/09/2026 | 16/09/2026 | <https://docs.aws.amazon.com/cost-management/> |
| **5** | - Cài đặt **AWS CLI v2**, Git và Python 3.12 trên máy trạm Windows.<br>- Thực hành cấu hình profile (`aws configure` / `aws login`) cho vùng `ap-southeast-1`. | 17/09/2026 | 17/09/2026 | <https://docs.aws.amazon.com/cli/> |
| **6** | - Thực hành lệnh AWS CLI cơ bản (`sts get-caller-identity`, `ec2 describe-regions`).<br>- Hoàn thiện ghi chú Worklog Tuần 1. | 18/09/2026 | 18/09/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 1

* Hoàn tất thiết lập tài khoản AWS bảo mật (MFA + IAM User + AWS Budgets cảnh báo chi tiêu sớm).
* Nắm vững thao tác song song trên AWS Management Console và AWS CLI v2 tại vùng `ap-southeast-1` (Singapore).
* Hiểu rõ yêu cầu OJT của FCAJ để lên kế hoạch triển khai sản phẩm và viết blog cộng đồng.
