---
title: "Worklog Tuần 4"
date: 2026-11-23
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Kiểm tra và điều chỉnh lại chi tiết công việc từng ngày cho khớp 100% với lịch cá nhân của bạn nếu cần.
{{% /notice %}}

### Mục tiêu tuần 4 (05/10/2026 – 09/10/2026)

* Hoàn thành **Module 03 (Phần 2 — Storage Gateway & S3/CloudFront)**: `Lab 24` & `Lab 57`.
* Hoàn thành **Module 04 (Phần 1 — Dịch vụ Lưu trữ AWS, S3 Backup & VM Import/Export)**: `04-01` → `04-04`, `Lab 13` & `Lab 14`.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu (Khóa học FCAJ) |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - **Thực hành Module 03-Lab24 & Module 03-Lab57 (Phần 1):** Cấu hình S3 + EC2 Storage Gateway (`Lab 24`); Tạo S3 Bucket, Static Website, Block Public Access (`Lab 57`). | 05/10/2026 | 05/10/2026 | - [03-Lab24 Storage Gateway](https://www.youtube.com/watch?v=Je2jPk7HhLQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [03-Lab57-03 Static Website](https://www.youtube.com/watch?v=9Cd_dAUCh9o&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [03-Lab57-04 Public Access Block](https://www.youtube.com/watch?v=iw0qEi-PiOc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **3** | - **Thực hành Module 03-Lab57 (07.1 → 11):** Chặn toàn bộ Public Access, cấu hình **Amazon CloudFront**, Bucket Versioning, Multi-Region Object Replication & Clean up. | 06/10/2026 | 06/10/2026 | - [03-Lab57-07.2 CloudFront](https://www.youtube.com/watch?v=5RxYavHbgVE&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [03-Lab57-08 Versioning](https://www.youtube.com/watch?v=HcLBLpYHtCw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [03-Lab57-10 Replication](https://www.youtube.com/watch?v=rSSZOhZnoHk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **4** | - Học lý thuyết **Module 04 (04-01 → 04-04):** Amazon S3 Access Point, Storage Classes, CORS, Object Key Performance, Glacier, Snow Family, Storage Gateway & Backup. | 07/10/2026 | 07/10/2026 | - [04-02 S3 & Storage Class](https://www.youtube.com/watch?v=_yunukwcAwc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [04-03 S3 CORS & Glacier](https://www.youtube.com/watch?v=mPBjB6Ltl_Q&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [04-04 Snow Family](https://www.youtube.com/watch?v=YXn8Q_Hpsu4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **5** | - **Thực hành Module 04-Lab13 (02.1 → 06) & Module 04-Lab57:** S3 Bucket + Backup Plan + Notifications + Test Restore; ôn tập CloudFront trên S3. | 08/10/2026 | 08/10/2026 | - [04-Lab13-03 Backup Plan](https://www.youtube.com/watch?v=cmIMSqeqPr4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [04-Lab13-05 Test Restore](https://www.youtube.com/watch?v=fZeMSyE0Spc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [04-Lab57-7.2 CloudFront](https://www.youtube.com/watch?v=n3uovWBqA88&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **6** | - **Thực hành Module 04-Lab14 (01 → 05) & Module 04-Lab24:** Export/Import VM từ On-premises lên AWS AMI (VMWare Workstation -> S3 -> EC2) & dọn dẹp tài nguyên. | 09/10/2026 | 09/10/2026 | - [04-Lab14-02.3 Import VM](https://www.youtube.com/watch?v=bsbQQZ3wDzY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [04-Lab14-02.4 Deploy AMI](https://www.youtube.com/watch?v=Yi60WeqqNWw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [04-Lab14-05 Clean Up](https://www.youtube.com/watch?v=Ipql97gmQjk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |

### Kết quả đạt được tuần 4

* Làm chủ mô hình phân phối nội dung tĩnh an toàn: **S3 Block All Public Access kết hợp Amazon CloudFront** (nền tảng trực tiếp cho Frontend của dự án SEAL Hackathon).
* Hiểu rõ các lớp lưu trữ S3, Versioning, Replication đa vùng và quy trình Backup/Restore tự động.
* Thực hành trọn vẹn quy trình Migration VM On-premises lên AWS qua `Lab 14`.
