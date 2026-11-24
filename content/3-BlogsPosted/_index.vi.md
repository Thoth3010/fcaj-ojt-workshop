---
title: "Các bài blogs đã đăng"
date: 2026-11-23
weight: 3
chapter: false
pre: " <b> 3. </b> "
---


### Danh sách 3 Bài Blogs Kỹ Thuật (AWS Study Group)

1. **[Blog 1 - Chiến lược Tối ưu Chi phí khi Triển khai Local LLM (Qwen3) trên AWS EC2 GPU kết hợp Amazon SQS](3.1-Blog1/)**
   - Phân tích bài toán tốn `$380–$720/tháng` nếu bật GPU EC2 24/7 và giải pháp dùng hàng đợi **Amazon SQS** tách luồng để bật/tắt EC2 theo đợt + lượng tử hóa `KV Cache (q8_0)` giảm 50% VRAM.
   - *Trạng thái link:* [Facebook post](https://www.facebook.com/share/p/1FJJYqU4Rp/)

2. **[Blog 2 - Thiết kế Pipeline Bất đồng bộ Chịu lỗi với Amazon SQS, Dead-Letter Queue (DLQ) và Amazon S3 Idempotency](3.2-Blog2/)**
   - Chia sẻ kinh nghiệm xây dựng hợp đồng thông điệp (`fcaj.ai.message.v1`), cơ chế `VisibilityTimeout` + Heartbeat, `RedrivePolicy` đẩy lỗi sang DLQ và ghi S3 an toàn với `If-None-Match: "*"`.
   - *Trạng thái link:* [Facebook post](https://www.facebook.com/share/p/1BYTn5tpyW/)

3. **[Blog 3 - Bảo mật Ứng dụng AI trên AWS: IAM Least Privilege, SSM Parameter Store và Chống rò rỉ Secret](3.3-Blog3/)**
   - Hướng dẫn áp dụng nguyên tắc quyền tối thiểu cho Lambda/EC2 AI Worker, bảo vệ API key bằng `SSM SecureString`, chống Prompt Injection và tự động che mật khẩu (`redact_secrets`) trong kết quả AI.
   - *Trạng thái link:* [Facebook post](https://www.facebook.com/share/p/19vbHFir6p/)
