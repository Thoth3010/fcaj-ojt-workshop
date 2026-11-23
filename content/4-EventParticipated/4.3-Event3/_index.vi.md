---
title: "Event 3"
date: 2026-11-23
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

{{% notice warning %}}
📝 **`[TODO - Viết lại sau]`:** Điền tên sự kiện thực tế #3 bạn đã tham gia, ngày giờ, địa điểm chính xác và thêm ảnh check-in rõ mặt vào `static/images/4-EventParticipated/event3-checkin.jpg`.
{{% /notice %}}

### Thông tin chung

- **Tên sự kiện:** `[TODO - Viết lại sau: Tên chính thức của Event 3 — VD: GenAI on AWS / AWS Security & Observability Workshop]`
- **Thời gian:** `[TODO - Viết lại sau: HH:mm, ngày dd/mm/2026]`
- **Địa điểm:** `[TODO - Viết lại sau: Văn phòng AWS Việt Nam / Địa điểm tổ chức / Online]`
- **Vai trò tham gia:** Người tham dự (Attendee)

---

### Nội dung chính tiếp thu

- `[TODO - Viết lại sau: Ghi lại nội dung các chủ đề chính đã tiếp thu trong Event 3]`
- Thực hành bảo mật cho ứng dụng AI trên Cloud: nguyên tắc **IAM Least Privilege**, quản lý bí mật qua **Systems Manager Parameter Store / Secrets Manager** và phòng chống Prompt Injection.
- Giám sát hệ thống đầu cuối bằng **Amazon CloudWatch Logs, Metrics & Alarms** kết hợp **Amazon SNS** để phát hiện sự cố sớm.

---

### Hình ảnh check-in rõ mặt chứng minh tham gia

> 📸 **`[TODO - Viết lại sau]`:** Đặt file ảnh check-in rõ mặt tại `static/images/4-EventParticipated/event3-checkin.jpg` và bỏ ghi chú để hiển thị:
>
> `![Check-in Event 3](/images/4-EventParticipated/event3-checkin.jpg)`

---

### Bài học rút ra & Đóng góp cá nhân

- Bổ sung bộ quy tắc **Security & Observability** vào Workshop cá nhân: tách quyền S3 theo từng prefix (`inputs/*`, `results/*`), thêm hàm `redact_secrets()` và tạo CloudWatch Alarm cảnh báo DLQ.
- Chia sẻ lại kinh nghiệm cấu hình Ollama + Qwen3 tối ưu `KV Cache (q8_0)` trên EC2 với các bạn cùng đợt thực tập.
