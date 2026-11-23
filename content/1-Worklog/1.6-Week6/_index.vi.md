---
title: "Worklog Tuần 6"
date: 2026-11-23
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Kiểm tra và điều chỉnh lại chi tiết công việc từng ngày cho khớp 100% với lịch cá nhân của bạn nếu cần.
{{% /notice %}}

### Mục tiêu tuần 6 (19/10/2026 – 23/10/2026)

* Tham gia thảo luận và chốt kế hoạch kiến trúc AWS (`docs/aws-workshop-architecture-plan.md`).
* Thiết kế hợp đồng dữ liệu JSON (`contracts/`) kết nối giữa Spring Boot Backend và Python AI Worker.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Tham gia review **AWS Workshop Architecture Plan**: tách frontend (S3+CloudFront), backend (EC2 Docker), DB (RDS) và AI Worker qua SQS. | 19/10/2026 | 19/10/2026 | `docs/aws-workshop-architecture-plan.md` |
| **3** | - Thiết kế cấu trúc `ai-worker/contracts/input_schema.json` & `output_schema.json` (rubric, commit SHA, criteria_results, evidence). | 20/10/2026 | 20/10/2026 | `ai-worker/contracts/` |
| **4** | - Thống nhất hợp đồng thông điệp bất đồng bộ `fcaj.ai.message.v1` với BE1/BE2 (`AI_JOB_REQUESTED`, `AI_JOB_COMPLETED`). | 21/10/2026 | 21/10/2026 | `docs/contracts/ai-job-v1/` |
| **5** | - Tính toán dự toán chi phí ban đầu bằng **AWS Pricing Calculator** đảm bảo mục tiêu tự vận hành PoC `< 500.000 VNĐ/tháng`. | 22/10/2026 | 22/10/2026 | <https://calculator.aws/> |
| **6** | - Hoàn thiện tài liệu Proposal và tạo skeleton thư mục `ai-worker/` (`src/`, `contracts/`, `tests/`). | 23/10/2026 | 23/10/2026 | `ai-worker/README.md` |

### Kết quả đạt được tuần 6

* Chốt xong kiến trúc AWS tổng thể 6 lớp và tách biệt hoàn toàn vai trò AI làm Technical Advisor.
* Hoàn thiện bộ JSON Schema đầu vào/đầu ra và mẫu `sample_input.json` / `sample_output.json` làm chuẩn tích hợp.
* Xây dựng xong bảng dự toán chi phí AWS Pricing Calculator cho giai đoạn PoC.
