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

* Hoàn thành **Module 07 (Phần 2 — Data Pipeline, Firehose, Glue, DataBrew, EMR, Athena, Kinesis, QuickSight & Lambda Serving)**: `Lab 35`, `Lab 70`, `Lab 72`, `Lab 73`.
* **Dự án SEAL Hackathon:** Chuyển đổi & chạy benchmark **Local AI (`Ollama + Qwen3`) trực tiếp trên AWS EC2 (`ap-southeast-1`)**, tối ưu `KV Cache q8_0` & dọn sạch tài nguyên về `$0.00`.

### Nhật ký công việc hàng ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu (Khóa học FCAJ & Dự án) |
| :-: | :--- | :---: | :---: | :--- |
| **2** | - **Thực hành Module 07-Lab35 (3.1 → 7):** S3 Bucket, Delivery Stream, Glue Crawler, Athena Analysis, QuickSight Visualization & Clean up.<br>- Soạn đề xuất **Local AI (Qwen3) trên AWS EC2** (`ec2_local_ai_proposal.md`). | 09/11/2026 | 09/11/2026 | - [07-Lab35-3.2 Delivery Stream](https://www.youtube.com/watch?v=a85LUgxpPUI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab35-4.1 Glue Crawler](https://www.youtube.com/watch?v=MQRJ_v8HYHM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/docs/ec2_local_ai_proposal.md` |
| **3** | - **Thực hành Module 07-Lab70 (1.1 → 2.3):** Tạo Cloud9 Instance, tải & upload dataset lên S3, Data Profiling & Clean/Transform với AWS Glue DataBrew.<br>- Viết script `setup_ec2_ollama.sh` (Swap 4GB, `OLLAMA_FLASH_ATTENTION=1`, `OLLAMA_KV_CACHE_TYPE=q8_0`, `shutdown -h +45`). | 10/11/2026 | 10/11/2026 | - [07-Lab70-2.1 DataBrew](https://www.youtube.com/watch?v=T-OPhEXdo9Y&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab70-2.3 Clean Data](https://www.youtube.com/watch?v=O-xRfw94xlY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/scripts/setup_ec2_ollama.sh` |
| **4** | - **Thực hành Module 07-Lab72 (2 → 8):** Ingest & Store, Catalog Data, Transform với AWS Glue (Interactive/GUI), DataBrew & EMR.<br>- Nâng cấp `ai_grader.py` hỗ trợ `provider="local_ai"` mặc định (`/no_think` + lọc `<think>`). | 11/11/2026 | 11/11/2026 | - [07-Lab72-5 Glue Interactive](https://www.youtube.com/watch?v=Eym-acAcD6s&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab72-8 Transform EMR](https://www.youtube.com/watch?v=PSBYrhMW-8g&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/src/ai_grader.py` |
| **5** | - **Thực hành Module 07-Lab72 (9 → 13) & Lab73 (3 → 5):** Athena, Kinesis Analytics, QuickSight, **Serve with Lambda**, Redshift & Interactive Dashboard.<br>- Khởi tạo EC2 Ubuntu 24.04 (`t3.small` Free Tier `ap-southeast-1`), kéo Qwen3 (`8.97s–11.59s`) và đo E2E JSON (`50.77s`, 100% pass). | 12/11/2026 | 12/11/2026 | - [07-Lab72-12 Serve with Lambda](https://www.youtube.com/watch?v=TZUA_0gSlNA&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab73-5 Interactive Dashboard](https://www.youtube.com/watch?v=KrTFP_qa0Ww&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/docs/ec2_local_ai_benchmark_report.md` |
| **6** | - Chạy `13/13` Unit Tests PASS (`0.032s`), Terminate toàn bộ EC2/EBS/SG/KeyPair về **`$0.00`** và nộp báo cáo benchmark cho Lead. | 13/11/2026 | 13/11/2026 | - `ai-worker/docs/ec2_local_ai_benchmark_report.md`<br>- [07-Lab35-7 Clean Up](https://www.youtube.com/watch?v=r9NehOtENWQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |

### Kết quả đạt được tuần 9

* Hoàn thành 100% **Module 07 (Data & Analytics Pipeline + Lambda Serving)** — khép lại toàn bộ 200+ bài giảng video lý thuyết và thực hành trong khóa học First Cloud Journey.
* Chứng minh chạy thành công **Local AI (`Ollama + Qwen3`) trên AWS EC2 `ap-southeast-1`** đạt 100% JSON Schema & chi phí `$0.00` sau dọn dẹp.
