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

* Hiểu sâu về mạng ảo trên AWS: **Amazon VPC**, Subnet Public/Private, Route Table, Internet Gateway và NAT Gateway.
* Thực hành khởi tạo, kết nối và quản trị máy ảo **Amazon EC2** an toàn (Security Group & SSM Session Manager).

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Nghiên cứu kiến trúc **Amazon VPC**: CIDR block, Public vs Private Subnet trên nhiều Availability Zone. | 21/09/2026 | 21/09/2026 | <https://docs.aws.amazon.com/vpc/> |
| **3** | - Thực hành tạo VPC (`10.20.0.0/16`), Internet Gateway, Route Tables và cấu hình Security Group theo nguyên tắc đóng port mặc định. | 22/09/2026 | 22/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| **4** | - Tìm hiểu **Amazon EC2**: Instance Families (`t3`, `m7i-flex`, `g4dn` GPU), EBS `gp3`, On-Demand vs Spot Instance. | 23/09/2026 | 23/09/2026 | <https://docs.aws.amazon.com/ec2/> |
| **5** | - Thực hành khởi tạo EC2 Ubuntu 24.04 LTS, cấu hình UserData và kết nối không cần mở Port 22 qua **AWS Systems Manager Session Manager**. | 24/09/2026 | 24/09/2026 | <https://docs.aws.amazon.com/systems-manager/> |
| **6** | - Thực hành dọn dẹp tài nguyên lab (Terminate EC2, xóa EBS Volume, Security Group, VPC thử nghiệm) và kiểm tra hóa đơn `$0.00`. | 25/09/2026 | 25/09/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 2

* Thiết kế và dựng được mạng VPC phân tách Public/Private Subnet chuẩn multi-AZ.
* Triển khai thành công máy ảo EC2 Ubuntu và kết nối quản trị bảo mật qua SSM Session Manager mà không mở cổng SSH (22).
* Nắm vững thói quen dọn dẹp tài nguyên ngay sau khi thực hành xong.
