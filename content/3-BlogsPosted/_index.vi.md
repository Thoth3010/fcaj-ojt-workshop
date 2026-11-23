---
title: "Các bài blogs đã đăng"
date: 2026-11-23
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Theo quy định FCAJ, bạn cần đăng **tối thiểu 3 bài blogs chất lượng** lên nhóm cộng đồng [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj). Mình đã soạn sẵn nội dung kỹ thuật đầy đủ cho 3 bài blog gắn với đề tài của bạn dưới đây — bạn chỉ cần đăng lên nhóm rồi bổ sung **Link bài đăng thật** vào từng trang Blog 1, 2, 3 nhé!
{{% /notice %}}

### Danh sách 3 Bài Blogs Kỹ Thuật (AWS Study Group)

1. **[Blog 1 - Chiến lược Tối ưu Chi phí khi Triển khai Local LLM (Qwen3) trên AWS EC2 GPU kết hợp Amazon SQS](3.1-Blog1/)**
   - Phân tích bài toán tốn `$380–$720/tháng` nếu bật GPU EC2 24/7 và giải pháp dùng hàng đợi **Amazon SQS** tách luồng để bật/tắt EC2 theo đợt + lượng tử hóa `KV Cache (q8_0)` giảm 50% VRAM.
   - *Trạng thái link:* `[TODO - Viết lại sau: Bổ sung link bài đăng Facebook/Blog trên AWS Study Group]`

2. **[Blog 2 - Thiết kế Pipeline Bất đồng bộ Chịu lỗi với Amazon SQS, Dead-Letter Queue (DLQ) và Amazon S3 Idempotency](3.2-Blog2/)**
   - Chia sẻ kinh nghiệm xây dựng hợp đồng thông điệp (`fcaj.ai.message.v1`), cơ chế `VisibilityTimeout` + Heartbeat, `RedrivePolicy` đẩy lỗi sang DLQ và ghi S3 an toàn với `If-None-Match: "*"`.
   - *Trạng thái link:* `[TODO - Viết lại sau: Bổ sung link bài đăng Facebook/Blog trên AWS Study Group]`

3. **[Blog 3 - Bảo mật Ứng dụng AI trên AWS: IAM Least Privilege, SSM Parameter Store và Chống rò rỉ Secret](3.3-Blog3/)**
   - Hướng dẫn áp dụng nguyên tắc quyền tối thiểu cho Lambda/EC2 AI Worker, bảo vệ API key bằng `SSM SecureString`, chống Prompt Injection và tự động che mật khẩu (`redact_secrets`) trong kết quả AI.
   - *Trạng thái link:* `[TODO - Viết lại sau: Bổ sung link bài đăng Facebook/Blog trên AWS Study Group]`
