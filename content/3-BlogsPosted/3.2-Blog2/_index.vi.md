---
title: "Blog 2 - Pipeline Bất đồng bộ với SQS, DLQ & S3 Idempotency"
date: 2026-11-23
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

{{% notice info %}}
🔗 **Link bài đăng AWS Study Group:** [Facebook post](https://www.facebook.com/share/p/1BYTn5tpyW/)
{{% /notice %}}

# Thiết kế Pipeline Xử lý Bất đồng bộ Chịu lỗi (Fault-Tolerant) với Amazon SQS, Dead-Letter Queue (DLQ) và Amazon S3 Idempotency

Khi tích hợp AI vào các ứng dụng web thực tế, thời gian xử lý một request thường kéo dài từ `15` đến `60` giây. Nếu giữ kết nối HTTP đồng bộ, người dùng dễ gặp lỗi timeout và hệ thống không thể chịu được tải đột biến. Dưới đây là những bài học thực tế khi thiết kế đường ống bất đồng bộ trên AWS cho dự án **SEAL Hackathon**.

---

## 1. Kiến trúc 2 Hàng đợi + 2 Dead-Letter Queues (DLQ)

Hệ thống tách biệt hai chiều giao tiếp giữa Backend và AI Worker:
- **`fcaj-ai-jobs-queue` (+ `fcaj-ai-jobs-dlq`):** Backend gửi yêu cầu `AI_JOB_REQUESTED`, worker nhận và xử lý.
- **`fcaj-ai-results-queue` (+ `fcaj-ai-results-dlq`):** Worker báo kết quả `AI_JOB_COMPLETED`, Backend cập nhật DB.

Việc cấu hình **`RedrivePolicy` với `maxReceiveCount = 3`** đảm bảo một thông điệp bị lỗi định dạng (poison message) hoặc sập worker sẽ chỉ thử lại tối đa 3 lần trước khi tự động chuyển sang **DLQ**, tránh vòng lặp vô tận làm tiêu tốn token LLM và tài nguyên Lambda/EC2.

---

## 2. Xử lý bài toán Duplicate Message & Visibility Timeout

Trong **Amazon SQS Standard Queue**, cơ chế đảm bảo là *At-Least-Once Delivery* (một message có thể được giao hơn 1 lần) và nếu quá thời gian `VisibilityTimeout` mà worker chưa xóa message, SQS sẽ phát lại cho worker khác. Để đảm bảo **không ghi đè hoặc chấm trùng kết quả**, nhóm áp dụng 3 nguyên tắc:

1. **Tách dữ liệu lớn sang Amazon S3 (Claim-Check Pattern):** SQS chỉ chứa metadata nhẹ (`fcaj.ai.message.v1`, `< 32 KB`) kèm đường dẫn và mã băm **SHA-256** của `source.json` và `rubric.json` trên S3.
2. **Gia hạn Visibility Timeout tự động (SQS Heartbeat):** Khi worker chạy suy luận Local AI trên EC2 (có thể mất 30–50 giây), luồng nền định kỳ gọi `sqs.change_message_visibility()` để gia hạn thời gian giữ job trước khi hết hạn.
3. **Ghi S3 Idempotent bằng `If-None-Match: "*"`:**
   ```python
   s3_client.put_object(
       Bucket=bucket,
       Key=f"{prefix}/results/{job_id}/output.json",
       Body=payload_bytes,
       ContentType="application/json",
       IfNoneMatch="*",
   )
   ```
   Nhờ header `IfNoneMatch="*"` của Amazon S3, nếu hai worker vô tình chạy trùng cùng một `jobId`, chỉ ghi thành công duy nhất một lần và tuyệt đối không ghi đè sai lệch kết quả.

---

## 3. Giám sát độ trễ & Cảnh báo DLQ với CloudWatch

Khi kết hợp thêm **CloudWatch Alarm** theo dõi metric `ApproximateNumberOfMessagesVisible > 0` trên hai hàng đợi DLQ nối tới **Amazon SNS**, đội ngũ vận hành lập tức nhận được email cảnh báo ngay khi có bất kỳ job AI nào thất bại sau 3 lần retry để kiểm tra và redrive an toàn.
