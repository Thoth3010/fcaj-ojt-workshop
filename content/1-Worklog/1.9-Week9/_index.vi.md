---
title: "Worklog Tuần 9"
date: 2026-11-23
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

{{% notice info %}}
📝 **`[TODO - Viết lại sau]`:** Kiểm tra và điều chỉnh lại chi tiết công việc từng ngày cho khớp 100% với lịch cá nhân của bạn nếu cần.
{{% /notice %}}

### Mục tiêu tuần 9 (09/11/2026 – 13/11/2026)

* Nghiên cứu phương án chạy **Local AI (`Ollama + Qwen3`) trực tiếp trên AWS EC2** để bảo mật tuyệt đối mã nguồn trong VPC.
* Khởi tạo máy ảo EC2 tại `ap-southeast-1`, benchmark hiệu năng Qwen3, tối ưu `KV Cache (q8_0)` và dọn sạch tài nguyên về `$0.00`.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - Soạn đề xuất kiến trúc **Local AI (Qwen3) trên AWS EC2** (`ec2_local_ai_proposal.md`), đối chiếu `Qwen3-14B` (`g4dn.xlarge`) và `Qwen3-30B-A3B MoE` (`g5.xlarge`). | 09/11/2026 | 09/11/2026 | `ai-worker/docs/ec2_local_ai_proposal.md` |
| **3** | - Viết script tự động `setup_ec2_ollama.sh` cấu hình Swap 4GB, `OLLAMA_FLASH_ATTENTION=1`, `OLLAMA_KV_CACHE_TYPE=q8_0`, `shutdown -h +45`. | 10/11/2026 | 10/11/2026 | `ai-worker/scripts/setup_ec2_ollama.sh` |
| **4** | - Nâng cấp `ai_grader.py` hỗ trợ `provider="local_ai"` mặc định (`/v1/chat/completions`), chèn `/no_think` và regex lọc `<think>...</think>`. | 11/11/2026 | 11/11/2026 | `ai-worker/src/ai_grader.py` |
| **5** | - Khởi tạo EC2 Ubuntu 24.04 (`t3.small` Free Tier) tại `ap-southeast-1`, kéo `qwen3` (`8.97s–11.59s`), đo E2E JSON output (`50.77s`, 100% schema pass). | 12/11/2026 | 12/11/2026 | `ai-worker/docs/ec2_local_ai_benchmark_report.md` |
| **6** | - Chạy `13/13` Unit Tests PASS (`0.032s`), `Terminate` toàn bộ EC2/EBS/SG/KeyPair về `$0.00` và nộp báo cáo benchmark. | 13/11/2026 | 13/11/2026 | `ai-worker/docs/ec2_local_ai_benchmark_report.md` |

### Kết quả đạt được tuần 9

* Chứng minh tính khả thi của **Local AI (`Ollama + Qwen3`) trên AWS EC2** với độ tuân thủ JSON Schema 100% và khả năng che secret tự động.
* Tối ưu dung lượng VRAM/RAM thêm 50% nhờ `OLLAMA_KV_CACHE_TYPE=q8_0` kết hợp Smart Repo Slicing (`35,000` ký tự).
* Giữ chi phí kiểm thử thực tế trên AWS ở mức **`$0.00`** nhờ dọn dẹp tài nguyên triệt để ngay sau khi thu thập số liệu.
