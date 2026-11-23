---
title: "Worklog Tuần 10"
date: 2026-11-23
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Kiểm tra và điều chỉnh lại chi tiết công việc từng ngày cho khớp 100% với lịch cá nhân của bạn nếu cần.
{{% /notice %}}

### Mục tiêu tuần 10 (16/11/2026 – 20/11/2026)

* Hoàn thiện kiến trúc tích hợp **AWS v3**: xây dựng **`lambda_handler.py`** và **`sqs_worker.py`** theo đúng contract `fcaj.ai.message.v1` / `fcaj.ai.output.v1`.
* Triển khai cơ chế kiểm tra **SHA-256**, ghi S3 idempotent (`If-None-Match: "*"`) và đọc secret từ **SSM Parameter Store**.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Nghiên cứu tài liệu kiến trúc AWS v3 (`2aOboRCqu5DgDHelB6fUFKkeiAnJaYh3wF1DxO08.md`), chốt vị trí Lambda ngoài VPC kết hợp S3/SQS/SSM. | 16/11/2026 | 16/11/2026 | `ai-worker/README.md` |
| **3** | - Phát triển `src/lambda_handler.py`: kiểm định SHA-256 & `sizeBytes` cho `input-manifest.json`, `source.json`, `rubric.json` trên S3. | 17/11/2026 | 17/11/2026 | `ai-worker/src/lambda_handler.py` |
| **4** | - Tích hợp SSM Parameter Store cache warm-start (`_CACHED_DEEPSEEK_API_KEY`), hậu kiểm `safeText` và ghi S3 `If-None-Match: "*"`. | 18/11/2026 | 18/11/2026 | `ai-worker/src/lambda_handler.py` |
| **5** | - Xây dựng `src/sqs_worker.py` hỗ trợ Long Polling (`WaitTimeSeconds=20`), `VisibilityTimeout=120s` và credential ngắn hạn qua `aws login`. | 19/11/2026 | 19/11/2026 | `ai-worker/src/sqs_worker.py` |
| **6** | - Viết và chạy pass toàn bộ test hợp đồng v3 (`tests/test_lambda_handler_v1.py`, `tests/test_sqs_worker.py`). | 20/11/2026 | 20/11/2026 | `ai-worker/tests/` |

### Kết quả đạt được tuần 10

* Hoàn thiện cả 2 chế độ vận hành sản xuất: **AWS Lambda Worker (Serverless)** và **Standalone/EC2 SQS Polling Worker**.
* Đảm bảo tính toàn vẹn dữ liệu đầu vào/ra bằng SHA-256 và idempotency tuyệt đối khi SQS phát lại tin nhắn.
* Toàn bộ suite unit & contract tests (`test_ai_worker.py`, `test_lambda_handler_v1.py`, `test_sqs_worker.py`) chạy ổn định.
