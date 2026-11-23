---
title: "Event 2"
date: 2026-11-23
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

{{% notice warning %}}
📝 **`[TODO - Viết lại sau]`:** Điền tên sự kiện thực tế #2 bạn đã tham gia, ngày giờ, địa điểm chính xác và thêm ảnh check-in rõ mặt vào `static/images/4-EventParticipated/event2-checkin.jpg`.
{{% /notice %}}

### Thông tin chung

- **Tên sự kiện:** `[TODO - Viết lại sau: Tên chính thức của Event 2 — VD: Serverless & Event-Driven Architecture Workshop]`
- **Thời gian:** `[TODO - Viết lại sau: HH:mm, ngày dd/mm/2026]`
- **Địa điểm:** `[TODO - Viết lại sau: Văn phòng AWS Việt Nam / Địa điểm tổ chức / Online]`
- **Vai trò tham gia:** Người tham dự (Attendee)

---

### Nội dung chính tiếp thu

- `[TODO - Viết lại sau: Bổ sung nội dung chi tiết từ diễn giả tại Event 2]`
- Kiến trúc hướng sự kiện (Event-Driven Architecture) sử dụng **Amazon SQS**, **Dead-Letter Queue (DLQ)** và **AWS Lambda** để tách rời các tác vụ xử lý nặng.
- Chiến lược **Cost Optimization** cho ứng dụng thực tế: chọn mô hình Serverless (pay-per-use), tận dụng Spot Instance và thiết lập cảnh báo chi phí sớm qua CloudWatch & AWS Budgets.

---

### Hình ảnh check-in rõ mặt chứng minh tham gia

> 📸 **`[TODO - Viết lại sau]`:** Đặt file ảnh check-in rõ mặt tại `static/images/4-EventParticipated/event2-checkin.jpg` và bỏ ghi chú để hiển thị:
>
> `![Check-in Event 2](/images/4-EventParticipated/event2-checkin.jpg)`

---

### Bài học rút ra & Đóng góp cá nhân

- Áp dụng trực tiếp mô hình **SQS + DLQ + Idempotency** từ buổi chia sẻ vào thiết kế hệ thống **AI Judge Pipeline** cho dự án SEAL Hackathon.
- Tham gia đặt câu hỏi thảo luận về cách xử lý `VisibilityTimeout` khi tác vụ AI mất nhiều thời gian hơn cấu hình timeout mặc định.
