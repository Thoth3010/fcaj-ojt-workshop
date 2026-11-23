---
title: "Worklog Tuần 11"
date: 2026-11-23
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Kiểm tra và điều chỉnh lại chi tiết công việc từng ngày cho khớp 100% với lịch cá nhân của bạn nếu cần.
{{% /notice %}}

### Mục tiêu tuần 11 (23/11/2026 – 27/11/2026)

* Hoàn thiện hệ thống giám sát **CloudWatch Logs, Metrics, Alarms & Amazon SNS** cho pipeline AI Judge.
* Xây dựng toàn bộ website **Báo cáo thực tập & Workshop kỹ thuật cá nhân (song ngữ VI/EN)** theo chuẩn template FCAJ.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Rà soát 100% quy định nộp Workshop FCAJ (bảo mật IAM, bảng Cost Estimation, Well-Architected, CloudWatch, Clean-up, song ngữ). | 23/11/2026 | 23/11/2026 | <https://hcm-rules.awsfcaj.com/project> |
| **3** | - Thiết kế sơ đồ kiến trúc Proposal (6 lớp) và sơ đồ Workshop chi tiết luồng S3 + SQS + AI Worker + CloudWatch. | 24/11/2026 | 24/11/2026 | `static/images/` |
| **4** | - Viết hoàn chỉnh 3 bài Blog kỹ thuật (Cost Optimization Qwen3, SQS/DLQ Idempotency, IAM Least Privilege) để đăng AWS Study Group. | 25/11/2026 | 25/11/2026 | <https://www.facebook.com/groups/awsstudygroupfcj> |
| **5** | - Viết hướng dẫn thực hành Step-by-Step cho Workshop (`5.1` – `5.6`): CLI tạo S3/SQS/IAM/SSM, deploy Worker, CloudWatch Alarm & Clean-up. | 26/11/2026 | 26/11/2026 | `content/5-Workshop/` |
| **6** | - Triển khai website Hugo lên **GitHub Pages** qua GitHub Actions (`peaceiris/actions-hugo` & `actions-gh-pages`) và kiểm tra hiển thị VI/EN. | 27/11/2026 | 27/11/2026 | <https://docs.github.com/pages> |

### Kết quả đạt được tuần 11

* Website báo cáo thực tập & Workshop kỹ thuật cá nhân chạy ổn định trên GitHub Pages với đầy đủ 2 ngôn ngữ Việt/Anh.
* Bổ sung đầy đủ các mục bắt buộc theo tiêu chuẩn FCAJ: 12-week Worklog, Proposal + Cost Estimation, 3 Blogs, 3 Events, Workshop tái lập được từ đầu tới cuối.
