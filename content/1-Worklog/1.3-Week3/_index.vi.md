---
title: "Worklog Tuần 3"
date: 2026-11-23
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3 (28/09/2026 – 02/10/2026)

* Hoàn thành **Module 02 (Phần 2 — Kết nối Multi-VPC)**: `Lab 19` (VPC Peering) và `Lab 20` (AWS Transit Gateway).
* Hoàn thành **Module 03 (Phần 1 — Compute EC2 & AWS Backup)**: `03-01` → `03-02` và `Lab 13` (Deploy AWS Backup & Test Restore).

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu (Khóa học FCAJ) |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - **Thực hành Module 02-Lab19 (01 → 07):** Thiết lập VPC Peering bằng CloudFormation, cập nhật NACL, Route Tables, bật Cross-Peer DNS & dọn dẹp tài nguyên. | 28/09/2026 | 28/09/2026 | - [Lab19-01 VPC Peering](https://www.youtube.com/watch?v=sllYqAECBoM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [Lab19-04 Peering Connection](https://www.youtube.com/watch?v=drKX_FnW9r8&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [Lab19-06 Cross-Peer DNS](https://www.youtube.com/watch?v=H8o5TSzb_l4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **3** | - **Thực hành Module 02-Lab20 (01 → 07):** Tạo AWS Transit Gateway, Transit Gateway Attachments, Transit Gateway Route Tables & định tuyến Multi-VPC; Clean up.<br>- **Tham dự sự kiện Event 2 — AWS Cloud & AI Day Hanoi 2026:** Nghe chuyên đề về *Enterprise Knowledge Hub*, *Retrieval and Intelligence (RAG)*, *Security and Governance* và *Roadmap to Enterprise Adoption*. | 29/09/2026 | 29/09/2026 | - [Lab20-01 Transit Gateway](https://www.youtube.com/watch?v=ybLa49z7FFg&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [Lab20-04 Attachments](https://www.youtube.com/watch?v=ytlFy2M8Ow0&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [Lab20-06 VPC Routes](https://www.youtube.com/watch?v=QSXgL2KodQI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [Event 2: AWS Cloud & AI Day Hanoi 2026](../../4-eventparticipated/4.2-event2/) |
| **4** | - Học lý thuyết **Module 03 (03-01-01 → 03-01-07):** EC2 Instance Types, AMI/Backup/Key Pair, Elastic Block Store (EBS), Instance Store, User Data, Metadata & EC2 Auto Scaling. | 30/09/2026 | 30/09/2026 | - [03-01-01 EC2 Instance Type](https://www.youtube.com/watch?v=e7XeKdOVq40&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [03-01-03 EBS](https://www.youtube.com/watch?v=hKr_TfGP7NY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [03-01-05 User Data](https://www.youtube.com/watch?v=_v_43Wi7zjo&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **5** | - Học **Module 03-02:** EC2 Auto Scaling nâng cao, EFS/FSx, Lightsail & AWS MGN. | 01/10/2026 | 01/10/2026 | - [03-02 Auto Scaling & EFS/FSx](https://www.youtube.com/watch?v=hFVYG8WqfU0&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **6** | - **Thực hành Module 03-Lab13 (01 → 06):** Triển khai **AWS Backup** cho hạ tầng EC2/EBS, tạo Backup Plan, kiểm thử **Test Restore** & dọn dẹp tài nguyên. | 02/10/2026 | 02/10/2026 | - [Lab13-02.2 Deploy Infra](https://www.youtube.com/watch?v=OBWLgMUiy9s&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [Lab13-03 Backup Plan](https://www.youtube.com/watch?v=-1ivCChsGFo&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [Lab13-05 Test Restore](https://www.youtube.com/watch?v=nd-o5GP6tXg&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |

### Kết quả đạt được tuần 3

* Phân biệt rõ ưu nhược điểm giữa **VPC Peering** (kết nối 1-1) và **AWS Transit Gateway** (kiến trúc Hub-and-Spoke cho nhiều VPC).
* Nắm vững vòng đời EC2 (Instance Type, EBS vs Instance Store, User Data khởi tạo tự động và IMDS metadata).
* Triển khai và kiểm chứng phục hồi dữ liệu thành công với **AWS Backup (`Lab 13`)**.
* Tham dự **AWS Cloud & AI Day Hanoi 2026** (29/09/2026), tiếp thu kiến thức về **Enterprise Knowledge Hub**, **RAG**, **Security & Governance**.
