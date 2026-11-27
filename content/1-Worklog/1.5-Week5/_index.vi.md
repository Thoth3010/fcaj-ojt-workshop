---
title: "Worklog Tuần 5"
date: 2026-11-23
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5 (12/10/2026 – 16/10/2026)

* Hoàn thành **Module 04 (Phần 2 — Amazon FSx `Lab 25`)** và **Module 05 (Phần 1 — Security, IAM, KMS, Security Hub `Lab 18` & Lambda Start/Stop EC2 `Lab 22`)**.
* Chính thức **Khởi động dự án SEAL / FCAJ Hackathon System**, nhận vai trò **AI Engineer** phụ trách module `ai-worker/`.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu (Khóa học FCAJ & Dự án) |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - **Thực hành Module 04-Lab25 (2.2 → 13):** Tạo Multi-AZ SSD/HDD file system (Amazon FSx), Test & Monitor Performance, Deduplication, Shadow Copies, Scale throughput & Delete environment. | 12/10/2026 | 12/10/2026 | - [04-Lab25-2.2 SSD Multi-AZ](https://www.youtube.com/watch?v=4tA3kOTx_Eo&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [04-Lab25-4 Test Performance](https://www.youtube.com/watch?v=I62tZyFpBB8&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [04-Lab25-13 Delete Env](https://www.youtube.com/watch?v=GPi_Bd-GdFI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **3** | - Học lý thuyết **Module 05 (05-01 → 05-08):** Shared Responsibility Model, AWS IAM, Amazon Cognito, AWS Organizations, Identity Center, KMS & AWS Security Hub. | 13/10/2026 | 13/10/2026 | - [05-01 Shared Responsibility](https://www.youtube.com/watch?v=tsobAlSg19g&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [05-02 AWS IAM](https://www.youtube.com/watch?v=N_vlJGAqZxo&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [05-06 AWS KMS](https://www.youtube.com/watch?v=GMihNQojhZc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **4** | - **Thực hành Module 05-Lab18 & Module 05-Lab22:** Kích hoạt AWS Security Hub (`Lab 18`); Viết AWS Lambda kết hợp IAM Role & Tag tự động Start/Stop EC2 + Slack Webhook (`Lab 22`). | 14/10/2026 | 14/10/2026 | - [05-Lab18-02 Security Hub](https://www.youtube.com/watch?v=YnLo4MgOXyA&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [05-Lab22-4 Lambda Role](https://www.youtube.com/watch?v=7_1A2Jxl7_c&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [05-Lab22-5.1 Stop EC2](https://www.youtube.com/watch?v=-iGkIHh9mXo&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **5** | - **Dự án SEAL Hackathon:** Họp nhóm Kick-off, đọc SRS (`ProjectRequirements.md`), Use Case & quy trình chấm điểm của Ban Giám khảo. | 15/10/2026 | 15/10/2026 | - `docs/documents/ProjectRequirements.md`<br>- `docs/documents/Business_Rules.pdf` |
| **6** | - **Dự án SEAL Hackathon:** Phân tích bài toán **AI Judge Assistant** — xác định yêu cầu chấm mã nguồn tự động theo Rubric kèm trích dẫn dòng code và kiểm soát chi phí dưới `500.000 VNĐ/tháng`. | 16/10/2026 | 16/10/2026 | - `docs/proposals/`<br>- [05-Lab22-7 Clean Up](https://www.youtube.com/watch?v=HdcBW-eKJWk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |

### Kết quả đạt được tuần 5

* Hoàn thành học phần **Security Foundations** và nắm cách dùng **AWS Lambda + Tag** tự động tắt/mở EC2 tiết kiệm chi phí (`Lab 22`) — ý tưởng trực tiếp áp dụng vào quản lý EC2 AI Worker sau này.
* Nắm rõ yêu cầu nghiệp vụ dự án **SEAL Hackathon** và chốt phạm vi công việc cho module AI Judge (`ai-worker/`).
