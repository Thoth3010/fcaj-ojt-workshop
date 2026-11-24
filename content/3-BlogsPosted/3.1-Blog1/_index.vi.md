---
title: "Blog 1 - Tối ưu Chi phí Local LLM trên AWS EC2"
date: 2026-11-23
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

{{% notice info %}}
🔗 **Link bài đăng AWS Study Group:** [Facebook post](https://www.facebook.com/share/p/1FJJYqU4Rp/)
{{% /notice %}}

# Chiến lược Tối ưu Chi phí (Cost Optimization) khi Triển khai Local LLM (Qwen3) trên AWS EC2 GPU kết hợp Amazon SQS

Trong quá trình xây dựng trợ lý giám khảo AI cho hệ thống **SEAL Hackathon**, một bài toán thực tế được đặt ra là: *Làm thế nào để vận hành mô hình ngôn ngữ lớn (`Qwen3-14B` / `Qwen3-30B-A3B`) ngay trong VPC AWS để bảo mật mã nguồn bài thi nhưng vẫn giữ chi phí dưới mức `500.000 VNĐ/tháng` (`~$20/tháng`)?*

---

## 1. Thách thức chi phí khi chạy GPU EC2 truyền thống

Một EC2 GPU tiêu chuẩn tại Region `ap-southeast-1` (Singapore) như `g4dn.xlarge` (1x NVIDIA T4 16GB VRAM) có giá On-Demand khoảng **`$0.526/giờ`** (`~$383/tháng` nếu chạy 24/7), còn `g5.xlarge` (24GB VRAM) lên tới **`$1.006/giờ`**. Với các cuộc thi Hackathon diễn ra theo từng đợt chấm bài, máy chủ AI thực chất nhàn rỗi hơn 90% thời gian trong tháng.

---

## 2. Ba đòn bẩy tối ưu chi phí đã áp dụng

### Đòn bẩy 1: Tách luồng bằng Amazon SQS để bật/tắt EC2 theo nhu cầu (On-Demand Window)
Thay vì để Backend gọi HTTP đồng bộ tới máy chủ AI:
1. Backend đẩy thông điệp job (`fcaj.ai.message.v1`) vào **Amazon SQS (`fcaj-ai-jobs-queue`)** và trả `202 Accepted` cho giao diện.
2. Khi không có đợt chấm bài, **EC2 GPU Worker ở trạng thái `Stopped` (`$0/giờ` compute)**. Toàn bộ yêu cầu chấm được lưu giữ an toàn trong SQS (tối đa lên tới 14 ngày).
3. Đến khung giờ nghiệm thu hoặc chấm bài, EC2 được khởi động trong 1–2 giờ để tiêu thụ hết hàng đợi, kết hợp cơ chế tự tắt an toàn (`shutdown -h +45`) nếu quên tắt máy. Kết hợp **EC2 Spot Instance (`~$0.16–$0.20/giờ`, rẻ hơn 70%)**, chi phí 20 giờ chấm mỗi tháng chỉ còn **`$3.20 – $4.00`**.

### Đòn bẩy 2: Lượng tử hóa KV-Cache (`q8_0`) & Flash Attention
Để tránh phải nâng cấp từ `g4dn.xlarge` (16GB VRAM) lên `g5.xlarge` (24GB VRAM) đắt gấp đôi khi xử lý repo mã nguồn dài 16k tokens, Ollama trên EC2 được tinh chỉnh:
```ini
Environment="OLLAMA_FLASH_ATTENTION=1"
Environment="OLLAMA_KV_CACHE_TYPE=q8_0"
Environment="OLLAMA_KEEP_ALIVE=-1"
```
Cấu hình này giảm **~50% mức tiêu thụ VRAM của KV-Cache** mà vẫn giữ nguyên độ chính xác đánh giá mã nguồn.

### Đòn bẩy 3: Chế độ `/no_think` + Smart Repo Slicing
Các mô hình Reasoning như `Qwen3` mặc định sinh hàng nghìn token nháp trong cặp thẻ `<think>...</think>`, làm tăng gấp 2–3 lần thời gian giữ máy EC2. Bằng cách chèn directive `/no_think` kết hợp bộ lọc `code_cleaner.py` (loại bỏ `node_modules`, `lockfile` và giữ nguyên số thứ tự dòng), thời gian xử lý mỗi repo giảm **~65%**, giúp cùng một cửa sổ giờ chạy EC2 xử lý được gấp ba lần số lượng bài thi.

---

## 3. Kết luận
Kết hợp **kiến trúc hướng sự kiện (Amazon SQS)** với tối ưu tầng inference (`q8_0`, `/no_think`, `Smart Repo Slicing`) giúp giảm chi phí vận hành GPU từ **`$383/tháng`** xuống còn **`~$3.20 – $6.00/tháng`**, phù hợp hoàn toàn cho các dự án sinh viên và PoC doanh nghiệp vừa và nhỏ.
