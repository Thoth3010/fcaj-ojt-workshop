---
title: "Worklog Tuần 2"
date: 2026-11-23
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Kiểm tra và điều chỉnh lại chi tiết công việc từng ngày cho khớp 100% với lịch cá nhân của bạn nếu cần.
{{% /notice %}}

### Mục tiêu tuần 2 (21/09/2026 – 25/09/2026)

* Hoàn thành **Module 02 (Phần 1 — Mạng ảo Amazon VPC & Hybrid DNS)**: `02-01` → `02-03`, `Lab 03` (Subnets, Route Table, IGW, NAT Gateway, Security Group, NACL, EC2 Instance Connect Endpoint) và `Lab 10` (Route 53 Resolver Hybrid DNS).

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu (Khóa học FCAJ) |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Học lý thuyết **Module 02 (02-01 → 02-03):** Amazon VPC, VPC Security, Multi-VPC, VPN, Direct Connect & Load Balancer. | 21/09/2026 | 21/09/2026 | - [02-01 AWS VPC](https://www.youtube.com/watch?v=O9Ac_vGHquM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [02-02 VPC Security](https://www.youtube.com/watch?v=BPuD1l2hEQ4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [02-03 VPN & LB](https://www.youtube.com/watch?v=CXU8D3kyxIc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **3** | - **Thực hành Module 02-Lab03 (01.1 → 02.3):** Tìm hiểu Subnets, Route Table, IGW, NAT Gateway, Security Group, Network ACLs & VPC Resource Map. | 22/09/2026 | 22/09/2026 | - [Lab03-01.1 Subnets](https://www.youtube.com/watch?v=DHYgA94SefE&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [Lab03-02.1 Security Group](https://www.youtube.com/watch?v=B1qxOQLmavQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [Lab03-02.3 VPC Resource Map](https://www.youtube.com/watch?v=fZa_kQ69stI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **4** | - **Thực hành Module 02-Lab03 (03.1 → 04.5):** Tự tạo VPC, Subnet, IGW, Route Table, Security Group, EC2 trong Public/Private Subnet, NAT Gateway & EC2 Instance Connect Endpoint. | 23/09/2026 | 23/09/2026 | - [Lab03-03.1 Create VPC](https://www.youtube.com/watch?v=I-5gTPDCOI8&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [Lab03-04.1 EC2 in Subnets](https://www.youtube.com/watch?v=duJEdF_g1To&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [Lab03-04.5 EC2 Connect Endpoint](https://www.youtube.com/watch?v=7NjNTnXon5s&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **5** | - **Thực hành Module 02-Lab10 (01 → 05.1):** Thiết lập Hybrid DNS với Route 53 Resolver — Key Pair, CloudFormation Template, Security Group, RDGW & Outbound Endpoint. | 24/09/2026 | 24/09/2026 | - [Lab10-01 Hybrid DNS](https://www.youtube.com/watch?v=FGicpWOmMDI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [Lab10-02.2 CloudFormation](https://www.youtube.com/watch?v=EQ-5P6U7Ph4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [Lab10-05.1 Outbound Endpoint](https://www.youtube.com/watch?v=YRNb7bJFtQU&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **6** | - **Thực hành Module 02-Lab10 (05.2 → 06):** Cấu hình Route 53 Resolver Rules, Inbound Endpoints, kiểm thử kết quả phân giải DNS & Clean up toàn bộ tài nguyên. | 25/09/2026 | 25/09/2026 | - [Lab10-05.2 Resolver Rules](https://www.youtube.com/watch?v=3KwnJsVivOs&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [Lab10-05.4 Test Results](https://www.youtube.com/watch?v=r-00KoWbC8c&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [Lab10-06 Clean Up](https://www.youtube.com/watch?v=5lMR8zA_DXU&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |

### Kết quả đạt được tuần 2

* Thành thạo thiết kế mạng VPC chuẩn Public/Private Subnet, định tuyến qua IGW/NAT Gateway và kiểm soát lưu lượng bằng Security Group / NACL.
* Biết cách sử dụng **EC2 Instance Connect Endpoint** để kết nối private EC2 không cần Public IP.
* Hoàn tất triển khai và dọn dẹp sạch bài lab **Route 53 Resolver Hybrid DNS (`Lab 10`)**.
