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
* Áp dụng lại hướng dẫn **Vẽ kiến trúc AWS trên `draw.io`** & **Hướng dẫn làm workshop AWS** để xây dựng hoàn chỉnh website báo cáo & Workshop cá nhân song ngữ (VI/EN).

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu (Khóa học FCAJ & Quy định) |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Rà soát 100% quy định nộp Workshop FCAJ (bảo mật IAM Least Privilege, bảng Cost Estimation, Well-Architected, CloudWatch, Clean-up, song ngữ). | 23/11/2026 | 23/11/2026 | - <https://hcm-rules.awsfcaj.com/project><br>- [Hướng dẫn làm workshop](https://www.youtube.com/watch?v=mXRqgMr_97U&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **3** | - Thực hành theo video *Hướng dẫn vẽ kiến trúc AWS trên draw.io*: thiết kế sơ đồ 6 lớp cho Proposal và sơ đồ chi tiết Workshop (`S3 + SQS + AI Worker + CloudWatch`). | 24/11/2026 | 24/11/2026 | - [Vẽ kiến trúc draw.io](https://www.youtube.com/watch?v=l8isyDe-GwY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `static/images/` |
| **4** | - Biên soạn 3 bài Blog kỹ thuật (Cost Optimization Qwen3 trên EC2, SQS/DLQ Idempotency, IAM Least Privilege & Secret Redaction) chuẩn bị đăng AWS Study Group. | 25/11/2026 | 25/11/2026 | - <https://www.facebook.com/groups/awsstudygroupfcj><br>- `content/3-BlogsPosted/` |
| **5** | - Hoàn thiện hướng dẫn Step-by-Step cho Workshop (`5.1` – `5.6`): CLI tạo S3/SQS/IAM/SSM, deploy EC2/Lambda Worker, CloudWatch Alarm/SNS & Clean-up. | 26/11/2026 | 26/11/2026 | - `content/5-Workshop/`<br>- [01-Lab07 Cost Budget](https://www.youtube.com/watch?v=sd_KCcZOou0&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **6** | - Triển khai website Hugo lên **GitHub Pages** qua GitHub Actions, khôi phục phông chữ chuẩn `Amazon Ember` từ template gốc và kiểm tra giao diện VI/EN. | 27/11/2026 | 27/11/2026 | - <https://docs.github.com/pages><br>- <https://thoth3010.github.io/fcaj-ojt-workshop/> |

### Kết quả đạt được tuần 11

* Website báo cáo thực tập & Workshop kỹ thuật cá nhân live ổn định trên GitHub Pages với đầy đủ 2 ngôn ngữ Việt/Anh và đúng phông chữ chuẩn của template FCAJ.
* Đầy đủ mọi hạng mục bắt buộc: 12-week Worklog, Proposal + Cost Estimation, 3 Blogs, 3 Events và Workshop end-to-end tái lập được.
