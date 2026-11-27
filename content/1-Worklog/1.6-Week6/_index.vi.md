---
title: "Worklog Tuần 6"
date: 2026-11-23
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6 (19/10/2026 – 23/10/2026)

* Hoàn thành **Module 05 (Phần 2 — IAM Chuyên sâu, Tagging, KMS, CloudTrail & Athena)**: `Lab 27`, `Lab 28`, `Lab 30`, `Lab 33`, `Lab 44`, `Lab 48`.
* **Dự án SEAL Hackathon:** Chốt kế hoạch kiến trúc AWS (`aws-workshop-architecture-plan.md`), thiết kế JSON Contracts (`input_schema.json`, `output_schema.json`, `fcaj.ai.message.v1`) và bảng chi phí AWS Pricing Calculator.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu (Khóa học FCAJ & Dự án) |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - **Lab 05-Lab27 & Lab 05-Lab28:** Quản lý Resource Tags bằng CLI, tạo Resource Group; cấu hình IAM Policy/Role/Switch Roles & giới hạn quyền theo Tag.<br>- Họp nhóm chốt **AWS Workshop Architecture Plan** (`19/10/2026`). | 19/10/2026 | 19/10/2026 | - [05-Lab27-2.2 Tags CLI](https://www.youtube.com/watch?v=kYyceAFqsUg&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [05-Lab28-4 IAM Role](https://www.youtube.com/watch?v=pJWANviu8QM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `docs/aws-workshop-architecture-plan.md` |
| **3** | - **Lab 05-Lab30 & Lab 05-Lab44:** Viết Restriction Policy giới hạn IAM User, giới hạn Switch Role theo **IP & Time**.<br>- Thiết kế `ai-worker/contracts/input_schema.json` & `output_schema.json`. | 20/10/2026 | 20/10/2026 | - [05-Lab30-3 Restriction Policy](https://www.youtube.com/watch?v=MDDYZKU4i6Y&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [05-Lab44-4.3 Limit IP/Time](https://www.youtube.com/watch?v=asMebNbyISQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/contracts/` |
| **4** | - **Lab 05-Lab33:** Tạo KMS Key, mã hóa dữ liệu S3, bật CloudTrail logging và truy vấn log bằng **Amazon Athena**.<br>- Thống nhất hợp đồng `fcaj.ai.message.v1` với Backend BE1/BE2. | 21/10/2026 | 21/10/2026 | - [05-Lab33-3 KMS](https://www.youtube.com/watch?v=XdUKBuwEEr8&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [05-Lab33-5.4 Athena](https://www.youtube.com/watch?v=SWJDiY1fMjQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `docs/contracts/ai-job-v1/` |
| **5** | - **Lab 05-Lab48:** So sánh trực tiếp rủi ro khi dùng Access Key vs sử dụng **EC2 IAM Role** truy cập S3.<br>- Tính toán dự toán chi phí PoC bằng AWS Pricing Calculator. | 22/10/2026 | 22/10/2026 | - [05-Lab48-3.2 Using IAM Role](https://www.youtube.com/watch?v=Z0liKVSjt_Q&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [05-Lab48-4 Clean Up](https://www.youtube.com/watch?v=wl4wIo7UR9Y&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- <https://calculator.aws/> |
| **6** | - Khởi tạo cấu trúc thư mục `ai-worker/` (`src/`, `contracts/`, `tests/`, `docs/`) và hoàn thiện tài liệu Proposal kiến trúc cho nhóm. | 23/10/2026 | 23/10/2026 | - `ai-worker/README.md`<br>- [05-Lab33-7 Clean Up](https://www.youtube.com/watch?v=_EydymVG6UI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |

### Kết quả đạt được tuần 6

* Hoàn thành toàn bộ **Module 05 (Security & IAM Chuyên sâu)**: áp dụng triệt để **IAM Role thay cho Access Key** (`Lab 48`) và mã hóa KMS/CloudTrail (`Lab 33`) vào thiết kế dự án.
* Chốt kiến trúc 6 lớp cho **SEAL Hackathon Platform** và bộ JSON Schema chuẩn giao tiếp giữa Backend và AI Worker.
