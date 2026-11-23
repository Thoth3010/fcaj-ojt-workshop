---
title: "Worklog Tuần 12"
date: 2026-11-23
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Kiểm tra và điều chỉnh lại chi tiết công việc từng ngày cho khớp 100% với lịch cá nhân của bạn nếu cần (lưu ý quy định nộp Workshop **15 ngày trước ngày cần mộc**).
{{% /notice %}}

### Mục tiêu tuần 12 (30/11/2026 – 04/12/2026)

* Kiểm thử đầu cuối (E2E) & Fault Injection (DLQ -> CloudWatch Alarm -> SNS), quay video **Live Demo** sản phẩm thực tế.
* Hoàn tất dọn dẹp tài nguyên theo chuẩn Clean-up của khóa học FCAJ (`$0.00`), cập nhật đủ minh chứng 3 Blogs & 3 Events và nộp báo cáo OJT.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu (Khóa học FCAJ & Dự án) |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Diễn tập chạy thử E2E từ khâu đẩy job lên `fcaj-ai-jobs-queue` -> Lambda/EC2 Worker xử lý -> xuất `output.json` trên S3 & `fcaj-ai-results-queue`. | 30/11/2026 | 30/11/2026 | - `content/5-Workshop/5.5-Testing-Monitoring/` |
| **3** | - Kiểm thử kịch bản lỗi (Fault Injection): gửi message sai schema để xác nhận job nhảy sang `fcaj-ai-jobs-dlq` và kích hoạt **CloudWatch Alarm -> SNS Email**. | 01/12/2026 | 01/12/2026 | - <https://docs.aws.amazon.com/cloudwatch/> |
| **4** | - Quay video minh chứng Live Demo, cập nhật link 3 bài blog AWS Study Group, ảnh check-in rõ mặt 3 sự kiện và ảnh đại diện cá nhân. | 02/12/2026 | 02/12/2026 | - `content/3-BlogsPosted/`<br>- `content/4-EventParticipated/` |
| **5** | - Chạy toàn bộ quy trình **Clean-up tài nguyên** (Lambda, SQS/DLQ, empty & xóa S3 bucket, SSM, CloudWatch Alarm) và đối chiếu Billing `$0.00`. | 03/12/2026 | 03/12/2026 | - `content/5-Workshop/5.6-Cleanup/`<br>- [01-Lab07-06 Clean Up](https://www.youtube.com/watch?v=KeZi7eOLpOA&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **6** | - Rà soát tổng thể báo cáo song ngữ, gửi link website Workshop hoàn chỉnh cho chương trình FCAJ (đảm bảo trước ngày cần mộc ít nhất 15 ngày). | 04/12/2026 | 04/12/2026 | - <https://hcm-rules.awsfcaj.com/project> |

### Kết quả đạt được tuần 12

* Hoàn thành trọn vẹn chương trình **Workforce Bootcamp - First Cloud AI Journey (FCAJ)** và dự án **SEAL Hackathon System**.
* Sản phẩm AI Judge Pipeline vượt qua toàn bộ kiểm thử E2E, bảo mật, giám sát và dọn dẹp tài nguyên sạch sẽ (`$0.00`).
