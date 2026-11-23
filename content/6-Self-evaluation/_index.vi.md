---
title: "Tự đánh giá"
date: 2026-11-23
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Bảng dưới đây đã được điền sẵn đánh giá tham khảo dựa trên quá trình thực hiện đề tài SEAL Hackathon & AI Judge Worker. Bạn hãy rà soát và điều chỉnh lại mức **Tốt / Khá / Trung bình** và nhận xét cụ thể sao cho đúng nhất với bản thân trước khi nộp.
{{% /notice %}}

### Bảng Tự Đánh Giá Năng Lực Thực Tập (8 Tiêu Chí Bắt Buộc)

| STT | Tiêu chí đánh giá | Tự xếp loại | Nhận xét & Minh chứng cụ thể |
| :-: | :--- | :---: | :--- |
| 1 | **Kiến thức chuyên môn** | **Tốt** | Nắm vững các dịch vụ cốt lõi trên AWS (`EC2`, `VPC`, `IAM`, `S3`, `SQS`, `Lambda`, `RDS`, `SSM`, `CloudWatch`). Áp dụng kiến thức chuyên ngành AI để tích hợp mô hình Qwen3 (Ollama) và Cloud AI API (`DeepSeek` / `Gemini`) vào pipeline chấm mã nguồn bất đồng bộ đạt độ chính xác schema 100%. |
| 2 | **Khả năng tự học & nghiên cứu** | **Tốt** | Tự nghiên cứu kỹ thuật lượng tử hóa `KV Cache (q8_0)`, Flash Attention, cơ chế Grammar-Constrained JSON Output và các chuẩn thiết kế AWS Well-Architected Framework để tối ưu hóa tốc độ cũng như chi phí vận hành AI trên hạ tầng Free Tier và Spot Instance. |
| 3 | **Tính chủ động trong công việc** | **Tốt** | Chủ động phân tích rào cản VRAM, đề xuất giải pháp Smart Repo Slicing (`code_cleaner.py`) và chủ động thực hiện benchmark thực tế trên EC2 `ap-southeast-1` để nhóm có số liệu ra quyết định kiến trúc rõ ràng. |
| 4 | **Kỷ luật & tuân thủ quy định** | **Tốt** | Tuân thủ nghiêm ngặt quy tắc bảo mật (không hard-code credential, che secret tự động, dùng `IAM Least Privilege`, `SSM Parameter Store`), dọn dẹp tài nguyên sạch sẽ sau lab (`$0.00` chi phí ngoài dự kiến) và ghi nhận worklog đều đặn. |
| 5 | **Kỹ năng giao tiếp** | **Khá** | Trình bày và viết tài liệu kỹ thuật mạch lạc (báo cáo benchmark, proposal chuyển đổi Local AI, review code bằng cả tiếng Việt và tiếng Anh). Tiếp tục rèn luyện khả năng trình bày ngắn gọn, súc tích hơn khi demo sản phẩm trực tiếp. |
| 6 | **Làm việc nhóm (Teamwork)** | **Tốt** | Phối hợp chặt chẽ với Lead, Backend (BE1/BE2) và Frontend để thống nhất contract `fcaj.ai.message.v1` / `fcaj.ai.output.v1`, kiểm thử tích hợp end-to-end qua S3 và SQS mà không làm gián đoạn luồng làm việc của các thành viên khác. |
| 7 | **Năng lực giải quyết vấn đề** | **Tốt** | Giải quyết dứt điểm 4 bài toán kỹ thuật lớn: tràn ngữ cảnh repo 90k+ tokens (`Smart Repo Slicing`), lỗi LLM tính nhầm điểm trọng số (`Python post-processing`), lỗi rò rỉ secret trong snippet (`redact_secrets`), và rủi ro mất job khi timeout (`SQS Heartbeat` & `DLQ`). |
| 8 | **Đóng góp cho Workshop** | **Tốt** | Tự thiết kế và xây dựng hoàn chỉnh Workshop kỹ thuật cá nhân về hệ thống **Asynchronous AI Code Judge Pipeline trên AWS**, kèm script triển khai, bộ kiểm thử tự động (`13/13 PASS`), bảng dự toán chi phí và hướng dẫn dọn dẹp tài nguyên chi tiết. |

---

### Định Hướng Cải Thiện Sau Kỳ Thực Tập

- Mở rộng kinh nghiệm thực chiến với Infrastructure as Code (**Terraform / AWS CDK**) để tự động hóa hoàn toàn hạ tầng VPC, SQS, S3, Lambda và EC2 GPU chỉ bằng một lệnh.
- Nâng cao kỹ năng trình bày kỹ thuật bằng tiếng Anh và tối ưu hóa khả năng thiết kế hệ thống chịu tải cao (High-throughput Distributed Systems) kết hợp Cloud Observability chuyên sâu.
