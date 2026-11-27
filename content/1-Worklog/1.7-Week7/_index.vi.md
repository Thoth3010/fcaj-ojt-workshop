---
title: "Worklog Tuần 7"
date: 2026-11-23
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7 (26/10/2026 – 31/10/2026)

* Hoàn thành **Module 06 (Databases trên AWS)**: `06-01` → `06-03` (RDS, Aurora, Redshift, ElastiCache), `Lab 05` (VPC + EC2 + RDS & Backup/Restore) và `Lab 43` (AWS DMS & Schema Conversion).
* **Dự án SEAL Hackathon:** Phát triển `schema.py`, `code_cleaner.py` và đồng bộ `mock_worker.py` / `sample_output.json` với Backend BE1.
* Tham dự sự kiện **AWS First Cloud AI Journey Community Day 2026** (31/10/2026).

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu (Khóa học FCAJ & Dự án) |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Học lý thuyết **Module 06 (06-01 → 06-03):** Database Concepts, Amazon RDS & Aurora, Amazon Redshift & ElastiCache.<br>- Viết `src/schema.py` cho dự án SEAL. | 26/10/2026 | 26/10/2026 | - [06-01 Database Concepts](https://www.youtube.com/watch?v=OOD2RwWuLRw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [06-02 RDS & Aurora](https://www.youtube.com/watch?v=qbrobQZrokY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [06-03 Redshift & ElastiCache](https://www.youtube.com/watch?v=UvdiRW34aNI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **3** | - **Thực hành Module 06-Lab05 (2.1 → 7):** Tạo VPC, EC2/RDS Security Group, DB Subnet Group, RDS instance, triển khai app, Backup & Restore và Clean up.<br>- Viết `src/code_cleaner.py` lọc file & đánh số dòng. | 27/10/2026 | 27/10/2026 | - [06-Lab05-2.4 DB Subnet Group](https://www.youtube.com/watch?v=OWjX0FsbX9E&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [06-Lab05-4 Create RDS](https://www.youtube.com/watch?v=SlP-KdSs3IM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [06-Lab05-6 Backup & Restore](https://www.youtube.com/watch?v=7So4xNZJ6bk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **4** | - **Thực hành Module 06-Lab43 (01 → 10):** Kết nối Fleet Manager, cấu hình MSSQL/Oracle source, Schema Conversion sang Aurora MySQL.<br>- Cài đặt `_file_priority_key` trong `code_cleaner.py`. | 28/10/2026 | 28/10/2026 | - [06-Lab43-02 Fleet Manager](https://www.youtube.com/watch?v=nzvE2DYso38&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [06-Lab43-09 Schema Conv](https://www.youtube.com/watch?v=s-6mXTFXwG8&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/src/code_cleaner.py` |
| **5** | - **Thực hành Module 06-Lab43 (11 → 17):** Tạo Migration Task & Endpoint, Serverless Migration, Event Notifications, Logs & Troubleshoot Mem Pressure / Table Error.<br>- Đồng bộ `sample_output.json` & `mock_worker.py`. | 29/10/2026 | 29/10/2026 | - [06-Lab43-11 Migration Task](https://www.youtube.com/watch?v=4LoLN6D1UU8&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [06-Lab43-13 Serverless Migration](https://www.youtube.com/watch?v=tWGwAz_Ewk4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [06-Lab43-16 Troubleshoot Mem](https://www.youtube.com/watch?v=hB6vXJunUAY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **6** | - Chạy kiểm thử Local Mock Job bàn giao cùng Backend BE1 (xác nhận khớp `line_start`, `line_end` và dẫn chứng `criteria_id: 4`). | 30/10/2026 | 30/10/2026 | - `docs/report/local-mock-job-completion-2026-10-27.md`<br>- [06-Lab05-7 Clean Up](https://www.youtube.com/watch?v=0WiTedZTcpQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **7** | - **Tham dự sự kiện Event 3 — AWS First Cloud AI Journey Community Day 2026 (09:00 – 12:00):** Nghe các phiên *Building Software Factories*, *Education*, *AWS Lambda Web Functions*, *Amazon SQS: Building Asynchronous Systems*, *My 3-Month AWS Internship Journey* và *Open Source Contributing*. | 31/10/2026 | 31/10/2026 | - [Event 3: AWS First Cloud AI Journey Community Day 2026](../../4-eventparticipated/4.3-event3/) |

### Kết quả đạt được tuần 7

* Hoàn thành 100% **Module 06 (Databases)**: triển khai thành thạo RDS Private Subnet (`Lab 05`) và xử lý sự cố migration trên AWS DMS (`Lab 43`).
* Hoàn thiện bộ thu thập & chuẩn hóa mã nguồn (`code_cleaner.py`) + `mock_worker.py` nghiệm thu xong với nhóm Backend.
* Tham dự **AWS First Cloud AI Journey Community Day 2026**, cập nhật kiến thức về **AWS Lambda Web Functions**, **Amazon SQS** và văn hóa **Open Source**.
