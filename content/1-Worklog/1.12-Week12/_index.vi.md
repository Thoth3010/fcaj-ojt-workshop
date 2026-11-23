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

* Quay video / chuẩn bị **Live Demo** sản phẩm chạy thực tế (E2E job từ SQS -> AI Worker -> S3 Results -> CloudWatch Logs).
* Rà soát toàn bộ minh chứng (3 Blogs, 3 Events có ảnh check-in rõ mặt, 10 buổi lên văn phòng nếu xin mộc) và dọn dẹp sạch tài nguyên AWS.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Diễn tập chạy thử quy trình E2E từ khâu gửi job mẫu vào `fcaj-ai-jobs-queue` đến khi nhận output chuẩn xác trên S3 & `fcaj-ai-results-queue`. | 30/11/2026 | 30/11/2026 | `content/5-Workshop/5.5-Testing-Monitoring/` |
| **3** | - Kiểm tra kịch bản lỗi (fault injection): gửi message sai schema để xác nhận job nhảy sang DLQ và kích hoạt **CloudWatch Alarm -> SNS Email**. | 01/12/2026 | 01/12/2026 | <https://docs.aws.amazon.com/cloudwatch/> |
| **4** | - Quay video minh chứng Live Demo, cập nhật link blog AWS Study Group, ảnh check-in 3 sự kiện và ảnh đại diện cá nhân. | 02/12/2026 | 02/12/2026 | `content/` |
| **5** | - Chạy toàn bộ quy trình **Clean-up tài nguyên** (xóa Lambda, SQS/DLQ, empty & xóa S3 bucket, SSM, CloudWatch Alarm) và kiểm tra Billing `$0.00`. | 03/12/2026 | 03/12/2026 | `content/5-Workshop/5.6-Cleanup/` |
| **6** | - Hoàn tất rà soát lần cuối toàn bộ báo cáo song ngữ, nộp link Workshop website đúng hạn (trước ngày cần mộc ít nhất 15 ngày). | 04/12/2026 | 04/12/2026 | <https://hcm-rules.awsfcaj.com/project> |

### Kết quả đạt được tuần 12

* Hoàn thành 100% các hạng mục bắt buộc của báo cáo OJT FCAJ (chiếm 60% điểm OJT) đúng tiến độ.
* Hệ thống AI Judge Pipeline vượt qua đầy đủ các bài kiểm thử chức năng, bảo mật và giám sát thực tế.
* Tài khoản AWS được dọn dẹp sạch sẽ, không còn tài nguyên tồn đọng phát sinh chi phí.
