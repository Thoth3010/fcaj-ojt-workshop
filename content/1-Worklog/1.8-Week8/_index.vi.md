---
title: "Worklog Tuần 8"
date: 2026-11-23
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8 (02/11/2026 – 06/11/2026)

* Hoàn thành **Module 07 (Phần 1 — DynamoDB Serverless Event-Driven, Cost Tagging & AWS SDK)**: `Lab 39`, `Lab 40`, `Lab 60`.
* **Dự án SEAL Hackathon:** Xây dựng `ai_grader.py`, bảo mật `redact_secrets()`, chạy benchmark Cloud AI (`19.71s`) trên repo mẫu và viết bộ unit tests tự động.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu (Khóa học FCAJ & Dự án) |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - **Thực hành Module 07-Lab39 (1 → 5):** Hands-on Labs cho Amazon DynamoDB, khám phá Console, Backup & Clean up.<br>- Viết `SYSTEM_PROMPT` chuẩn hóa quy tắc trích dẫn chứng trong `ai_grader.py`. | 02/11/2026 | 02/11/2026 | - [07-Lab39-1 DynamoDB HOL](https://www.youtube.com/watch?v=w5bqLYPv6DA&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab39-4 Backup](https://www.youtube.com/watch?v=2nXUaTT1uoE&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/src/ai_grader.py` |
| **3** | - **Thực hành Module 07-Lab39 (6 → 8):** Advanced Design Patterns, Global Serverless App & **Serverless Event-Driven Architecture (LEDA)**.<br>- Bổ sung lớp phòng thủ chống Prompt Injection `<CANDIDATE_SOURCE_CODE>` & `redact_secrets()`. | 03/11/2026 | 03/11/2026 | - [07-Lab39-6 Advanced Patterns](https://www.youtube.com/watch?v=kTroCGJwA3g&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab39-7 Global Serverless](https://www.youtube.com/watch?v=eP_cB6SZQ1Q&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab39-8 Serverless LEDA](https://www.youtube.com/watch?v=F3fvIgeetGw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **4** | - **Thực hành Module 07-Lab40 (2.1 → 4):** Chuẩn bị DB, phân tích **Cost, Tagging & Cost Allocation**, Usage & Clean up.<br>- Cài đặt `compute_weighted_overall_score()` & chống tràn `max_tokens`. | 04/11/2026 | 04/11/2026 | - [07-Lab40-3.2 Cost](https://www.youtube.com/watch?v=vj53iTVV794&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab40-3.3 Tagging & Cost](https://www.youtube.com/watch?v=oFaX_1TggjQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab40-4 Clean Up](https://www.youtube.com/watch?v=ggFZt2JGIeM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **5** | - **Thực hành Module 07-Lab60 (1 → 3):** Thao tác AWS qua **CloudShell, Console và AWS SDK**.<br>- Chạy benchmark `lead-hackathon-test` (49 files, 7,257 dòng code) qua DeepSeek API (`19.71s`, `~$0.0175/job`). | 05/11/2026 | 05/11/2026 | - [07-Lab60-1 CloudShell](https://www.youtube.com/watch?v=cqczgtnvHjc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab60-3 AWS SDK](https://www.youtube.com/watch?v=gjY6l4elopw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/docs/ai_worker_review_and_decision_report.md` |
| **6** | - Viết và chạy pass 100% bộ kiểm thử tự động `tests/test_ai_worker.py` (`10/10` -> `13/13 PASS`). | 06/11/2026 | 06/11/2026 | - `ai-worker/tests/test_ai_worker.py` |

### Kết quả đạt được tuần 8

* Nắm vững thiết kế **Serverless Event-Driven Architecture (`Lab 39`)**, phân bổ chi phí theo Tag (`Lab 40`) và lập trình với AWS SDK (`Lab 60`).
* Hoàn thành lõi `ai_grader.py` đạt `19.71s/job` (`~$0.0175/job`), tự động che secret (`***REDACTED***`) và tính điểm trọng số chính xác bằng Python.
