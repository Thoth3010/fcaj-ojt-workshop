---
title: "Worklog Tuần 8"
date: 2026-11-23
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Kiểm tra và điều chỉnh lại chi tiết công việc từng ngày cho khớp 100% với lịch cá nhân của bạn nếu cần.
{{% /notice %}}

### Mục tiêu tuần 8 (02/11/2026 – 06/11/2026)

* Hoàn thiện module `ai_grader.py` tích hợp Cloud AI (`DeepSeek` / `Gemini`), hậu kiểm điểm số và bảo mật `redact_secrets`.
* Thực nghiệm benchmark trên repository thật (`lead-hackathon-test`) và viết bộ Unit Tests tự động.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Viết `SYSTEM_PROMPT` chuẩn hóa quy tắc trích dẫn chứng (`1–3 evidence/tiêu chí`), chống bịa số dòng và quy tắc `THIEU_DU_LIEU`. | 02/11/2026 | 02/11/2026 | `ai-worker/src/ai_grader.py` |
| **3** | - Triển khai hàng rào bảo mật: bọc `<CANDIDATE_SOURCE_CODE>` chống Prompt Injection, `strip_line_number_prefix()` và `redact_secrets()`. | 03/11/2026 | 03/11/2026 | `ai-worker/src/ai_grader.py` |
| **4** | - Cài đặt `compute_weighted_overall_score()` tính lại điểm trung bình trọng số bằng Python và kiểm tra `finish_reason == "length"`. | 04/11/2026 | 04/11/2026 | `ai-worker/src/schema.py` |
| **5** | - Chạy benchmark chấm repo mẫu `lead-hackathon-test` (49 files, 7,257 dòng code) qua DeepSeek API (`19.71s`, `~$0.0175/job`). | 05/11/2026 | 05/11/2026 | `ai-worker/docs/ai_worker_review_and_decision_report.md` |
| **6** | - Viết và chạy pass 100% bộ **Unit & Integration Tests** (`tests/test_ai_worker.py` — `10/10` -> `13/13 PASS`). | 06/11/2026 | 06/11/2026 | `ai-worker/tests/test_ai_worker.py` |

### Kết quả đạt được tuần 8

* Hoàn thành lõi `ai_grader.py` có khả năng tự động che mật khẩu/API key (`***REDACTED***`) và chống Prompt Injection.
* Loại bỏ 100% sai số cộng điểm trọng số nhờ hậu kiểm toán học bằng Python.
* Bộ kiểm thử tự động `test_ai_worker.py` đạt `100% PASS`, kèm báo cáo chi phí token thực tế (`~$0.0175/job`).
