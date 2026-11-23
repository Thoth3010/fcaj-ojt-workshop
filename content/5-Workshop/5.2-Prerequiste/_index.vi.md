---
title: "Điều kiện tiên quyết & Dự toán chi phí"
date: 2026-11-23
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

### 1. Điều kiện tiên quyết (Prerequisites)

Trước khi bắt đầu triển khai các bước trong Workshop, bạn cần chuẩn bị:

- **Tài khoản AWS:** Khuyến nghị sử dụng Region **`ap-southeast-1` (Singapore)** để tối ưu độ trễ kết nối từ Việt Nam; đã bật MFA và cài **AWS Budgets** cảnh báo chi tiêu (`$1` / `$5`).
- **Quyền IAM cần thiết:** IAM User/Role có quyền quản trị giới hạn cho Workshop (khởi tạo S3 bucket, SQS queue, SSM Parameter, IAM Role cho Worker, Lambda/EC2 và CloudWatch Alarm).
- **Công cụ trên máy cục bộ:**
  - **AWS CLI v2** (đã xác thực qua `aws login` hoặc `aws configure`)
  - **Python 3.12+** và **Git**
  - **Code mẫu AI Worker:** [fcaj-hackathon-system/ai-worker](file:///D:/FCAJ/fcaj-hackathon-system/ai-worker) (bao gồm `src/`, `scripts/`, `tests/`).

Kiểm tra nhanh môi trường trên Terminal trước khi bắt đầu:
```bash
aws --version
aws sts get-caller-identity --region ap-southeast-1
python --version
```

---

### 2. Bảng Dự toán Chi phí Chi tiết (AWS Pricing Calculator — `ap-southeast-1`)

{{% notice warning %}}
💰 **Hạng mục BẮT BUỘC (Cost Estimation):** Toàn bộ tính toán bên dưới được ước lượng theo **AWS Pricing Calculator** tại Region `ap-southeast-1` cho kịch bản thực tế **200 lượt chấm AI / tháng** (~1 đợt Hackathon 50 đội thi).
{{% /notice %}}

#### Kịch bản 1: Triển khai Workshop / Serverless Lab (Option B — AWS Lambda + S3 + SQS + CloudWatch)

| Dịch vụ AWS | Thông số cấu hình | Lưu lượng / Tháng | Đơn giá tham khảo | Chi phí / Tháng |
| :--- | :--- | :--- | :--- | :---: |
| **Amazon S3** | Standard Storage (`Private Bucket`), Block Public Access | `1 GB` lưu trữ, `2,000 PUT`, `4,000 GET` | `$0.025/GB` (Free Tier 5 GB năm đầu) | **$0.03** |
| **Amazon SQS** | 4 Standard Queues (`Jobs`, `Jobs-DLQ`, `Results`, `Results-DLQ`) | `~10,000 requests` | `$0.40 / 1M requests` (Always Free `1M` req) | **$0.00** |
| **AWS Lambda** | Python 3.12, `512 MB RAM`, trung bình `20s/job` | `200 invocations` (`2,000 GB-s`) | Always Free `400,000 GB-s` & `1M` req | **$0.00** |
| **SSM Parameter Store** | 1 Standard Parameter (`SecureString`) | `< 10,000 API calls` | Standard Parameter miễn phí | **$0.00** |
| **CloudWatch & SNS** | Log Group (Retention 14 ngày), `2 Standard Alarms`, Email SNS | `< 1 GB` logs, `2` alarms | Free Tier `5 GB` logs & `10` alarms | **$0.00** |
| **Cloud AI API (DeepSeek)** | `deepSeek-chat` (`~117k in / 4k out tokens` mỗi job) | `200 jobs` (Off-peak `$0.02/job`) | `$0.15/1M in`, `$0.60/1M out` | **~$3.50 – $4.00** |
| **TỔNG CỘNG (Serverless)** | | | | **~$3.53 – $4.03 / tháng** |

#### Kịch bản 2: Triển khai Local AI trên AWS EC2 (Option A — Không gửi code ra bên ngoài)

| Cấu hình EC2 (`ap-southeast-1`) | Thời gian bật/tháng | Chi phí Compute | EBS `30 GB gp3` | Tổng ước tính/tháng |
| :--- | :--- | :---: | :---: | :---: |
| **Free Tier Smoke Test (`t3.small` / `m7i-flex.large`)** | Chạy test lab 2 giờ rồi `Terminate` | `$0.00` (Free Tier) | `$0.00` | **$0.00** |
| **Production GPU Spot (`g4dn.xlarge` — 1x T4 16GB VRAM)** | Bật theo đợt chấm: **`20 giờ/tháng`** (`~$0.18/h` Spot) | `$3.60` | `$2.88` | **~$6.48 / tháng** |
| **So sánh nếu bật 24/7 On-Demand (`g4dn.xlarge`)** | `730 giờ/tháng` (`$0.526/h`) | `$383.98` | `$2.88` | **$386.86 / tháng** |

---

### 3. Chiến lược Tối ưu Chi phí (Cost Optimization)

1. **Tách hàng đợi SQS để tắt EC2 GPU khi nhàn rỗi (Giảm 98.4% tiền GPU):** Nhờ Amazon SQS lưu giữ message tối đa 14 ngày, EC2 GPU có thể ở trạng thái `Stopped` (`$0/giờ` compute) suốt thời gian không có đợt chấm, chỉ khởi chạy khi cần xử lý hàng đợi.
2. **Chốt chặn tự tắt Fail-safe trên EC2:** Script `setup_ec2_ollama.sh` tự động chèn lệnh `shutdown -h +45` để ngăn quên tắt máy sau khi demo.
3. **Lượng tử hóa KV-Cache (`q8_0`) & `/no_think`:** Cho phép chạy `Qwen3-14B` vừa khít trên `g4dn.xlarge` (16GB VRAM) thay vì phải thuê `g5.xlarge` đắt gấp đôi, đồng thời giảm 65% thời gian chạy mỗi job.
4. **S3 Lifecycle & Log Retention:** Tự động hết hạn (expire) các snapshot mã nguồn tạm sau 30 ngày trên S3 và giới hạn thời gian giữ log CloudWatch ở mức 7–14 ngày.
5. **AWS Free Tier & Lambda Concurrency Cap:** Giới hạn `MaximumConcurrency = 2` trên Lambda giúp vừa đủ trong hạn mức Free Tier vừa ngăn chặn hóa đơn tăng vọt nếu có sự cố retry.
