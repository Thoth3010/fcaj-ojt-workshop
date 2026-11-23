---
title: "Worklog Tuần 7"
date: 2026-11-23
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Kiểm tra và điều chỉnh lại chi tiết công việc từng ngày cho khớp 100% với lịch cá nhân của bạn nếu cần.
{{% /notice %}}

### Mục tiêu tuần 7 (26/10/2026 – 30/10/2026)

* Xây dựng module quét và làm sạch mã nguồn (`code_cleaner.py`) có đánh số dòng chính xác.
* Đồng bộ `schema.py`, `mock_worker.py` và rà soát contract với BE1 cho luồng tích hợp local & AWS.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Viết `src/schema.py` định nghĩa data models (`GradingJobInput`, `GradingJobOutput`, `CriterionResult`, `CodeEvidence`). | 26/10/2026 | 26/10/2026 | `ai-worker/src/schema.py` |
| **3** | - Viết `src/code_cleaner.py` lọc thư mục rác (`node_modules`, `target`, `.git`), file nhị phân, lockfile và đánh số từng dòng code. | 27/10/2026 | 27/10/2026 | `ai-worker/src/code_cleaner.py` |
| **4** | - Cài đặt cơ chế ưu tiên file code chính (`_file_priority_key` cho `src/`, `app/`, `back-end/`) và giới hạn `max_total_chars`. | 28/10/2026 | 28/10/2026 | `ai-worker/contracts/` |
| **5** | - Đồng bộ `sample_output.json` & `mock_worker.py`: sửa chính xác `line_start`, `line_end` và bổ sung dẫn chứng `criteria_id: 4`. | 29/10/2026 | 29/10/2026 | `ai-worker/src/mock_worker.py` |
| **6** | - Chạy kiểm thử mock integration handoff với Backend (BE1) và ghi nhận kết quả hoàn thiện local mock job. | 30/10/2026 | 30/10/2026 | `docs/report/local-mock-job-completion-2026-10-27.md` |

### Kết quả đạt được tuần 7

* Hoàn thiện pipeline thu thập và định dạng mã nguồn giữ nguyên số thứ tự dòng gốc.
* `mock_worker.py` và `sample_output.json` khớp 100% với cấu trúc dữ liệu thật của repository.
* Hoàn tất nghiệm thu bước Local Mock Job cùng nhóm Backend.
