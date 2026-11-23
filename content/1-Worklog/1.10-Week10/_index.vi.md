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

* Ôn tập & áp dụng thực chiến mẫu **Serverless Event-Driven (`07-Lab39`, `05-Lab22`)** và **IAM Role (`05-Lab48`)** vào **Kiến trúc AWS v3 của Dự án SEAL Hackathon**.
* Xây dựng hoàn chỉnh **`src/lambda_handler.py`** và **`src/sqs_worker.py`** theo đúng contract `fcaj.ai.message.v1` / `fcaj.ai.output.v1`.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu (Khóa học FCAJ & Dự án) |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Nghiên cứu kiến trúc mục tiêu **SEAL AWS v3** (`2aOboRCqu5DgDHelB6fUFKkeiAnJaYh3wF1DxO08.md`), ôn lại mẫu *Serve with Lambda* (`07-Lab72-12`) để đặt AI Worker ngoài VPC. | 16/11/2026 | 16/11/2026 | - `ai-worker/README.md`<br>- [07-Lab72-12 Serve with Lambda](https://www.youtube.com/watch?v=TZUA_0gSlNA&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **3** | - Phát triển `src/lambda_handler.py`: kiểm định toàn vẹn **SHA-256** & `sizeBytes` của `input-manifest.json`, `source.json`, `rubric.json` trên S3. | 17/11/2026 | 17/11/2026 | - `ai-worker/src/lambda_handler.py`<br>- [05-Lab48-3.2 Using IAM Role](https://www.youtube.com/watch?v=Z0liKVSjt_Q&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **4** | - Tích hợp **SSM Parameter Store** cache warm-start (`_CACHED_DEEPSEEK_API_KEY`), hậu kiểm `safeText` và ghi kết quả S3 **idempotent (`If-None-Match: "*"`)**. | 18/11/2026 | 18/11/2026 | - `ai-worker/src/lambda_handler.py`<br>- [07-Lab39-8 Serverless LEDA](https://www.youtube.com/watch?v=F3fvIgeetGw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **5** | - Xây dựng `src/sqs_worker.py` hỗ trợ Long Polling (`WaitTimeSeconds=20`), `VisibilityTimeout=120s` và xác thực credential ngắn hạn qua `aws login`. | 19/11/2026 | 19/11/2026 | - `ai-worker/src/sqs_worker.py`<br>- [05-Lab22-4 Lambda Role](https://www.youtube.com/watch?v=7_1A2Jxl7_c&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **6** | - Viết và chạy pass toàn bộ test hợp đồng v3 (`tests/test_lambda_handler_v1.py`, `tests/test_sqs_worker.py`). | 20/11/2026 | 20/11/2026 | - `ai-worker/tests/test_lambda_handler_v1.py`<br>- `ai-worker/tests/test_sqs_worker.py` |

### Kết quả đạt được tuần 10

* Hoàn thiện cả 2 chế độ vận hành sản xuất cho AI Worker: **AWS Lambda Serverless** và **EC2/Standalone SQS Poller**.
* Bảo đảm toàn vẹn dữ liệu (SHA-256) và chống ghi đè trùng lặp khi SQS phát lại tin nhắn (`If-None-Match: "*"`).
* Toàn bộ unit & contract tests chạy thông suốt không lỗi.
