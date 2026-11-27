---
title: "Chia sẻ, đóng góp ý kiến"
date: 2026-11-23
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

> Tham gia chương trình **First Cloud AI Journey (FCAJ)** là một bước đệm quan trọng giúp mình chuyển từ kiến thức lý thuyết tại **Đại học FPT** sang tư duy kỹ thuật thực tế theo chuẩn **AWS**. Chương trình không chỉ giúp mình hệ thống hóa kiến thức nền tảng về Cloud mà còn cập nhật rất sát các xu hướng mới về **Generative AI**, **RAG** và **Agentic AI** thông qua chuỗi bài học, cộng đồng và các sự kiện thực tế.

### Đánh giá chung

**1. Mức độ hài lòng tổng thể:** **Rất hài lòng (5/5)**.

Điều mình hài lòng nhất là có thể nối phần học và phần làm dự án với nhau. Khi làm lab, mình tập làm quen với từng dịch vụ. Đến dự án nhóm SEAL, mình phải nghĩ xem các dịch vụ phối hợp ra sao và làm thế nào để kiểm chứng luồng xử lý hoạt động đúng. Viết Worklog hằng tuần cũng giúp mình nhìn lại phần đã thực hành và phần cần làm thêm.

**2. Lộ trình học tập**\
Lộ trình học tập có cấu trúc rõ ràng từ nền tảng (`Cloud Foundations`, `VPC`, `EC2`, `S3`, `IAM`) đến các dịch vụ hiện đại (`Serverless`, `Event-Driven`, `AI/GenAI`).

Những buổi đầu giúp mình hiểu vai trò của mạng, phân quyền và lưu trữ trong một hệ thống AWS. Khi học đến Lambda và SQS, kiến thức đó giúp mình hiểu vì sao dự án SEAL tách khâu nhận bài nộp khỏi khâu chấm điểm bằng AI. Mình cũng có dịp triển khai và đo thời gian xử lý của mô hình chạy bằng Ollama và Qwen3 trên EC2.

**3. Bảo mật và quản trị chi phí**\
Luôn đề cao tư duy bảo mật và quản trị chi phí ngay từ những bài lab đầu tiên (`MFA`, `IAM Least Privilege`, `AWS Budgets` và dọn dẹp tài nguyên).

Các bài lab nhắc mình dành thời gian kiểm tra quyền IAM, đặt cảnh báo ngân sách và dọn tài nguyên. Với dự án chấm bài bằng AI, câu hỏi tương tự là worker cần truy cập dữ liệu nào và làm sao để tránh đưa thông tin nhạy cảm vào đầu vào mô hình. Phần xử lý dữ liệu trước khi chấm giúp mình thấy rõ bảo mật ảnh hưởng đến cách thiết kế luồng xử lý.

**4. Cộng đồng và sự kiện**\
Cộng đồng **AWS Study Group VN** và các buổi sự kiện trực tiếp (`Buildathon Kick-off`, `AWS Cloud & AI Day Hanoi`, `Community Day`) tạo môi trường kết nối cởi mở, giúp sinh viên được học hỏi trực tiếp từ các anh/chị mentor và kỹ sư đi trước.

Việc viết ba bài chia sẻ kỹ thuật cũng giúp mình học sâu hơn. Khi phải giải thích AWS MCP Server, IaC và AgentCore Harness cho người mới, mình cần đọc lại tài liệu và tìm cách diễn đạt rõ vai trò của từng công cụ. Đây là kỹ năng mình muốn tiếp tục rèn cùng với khả năng trình bày trực tiếp.

### Một số câu hỏi khác

- **Có giới thiệu chương trình cho bạn bè không? Vì sao?**\
  **Chắc chắn CÓ.**\
  **Lý do:** FCAJ mang lại môi trường học tập chủ động, gắn liền với thực tiễn doanh nghiệp và cập nhật công nghệ rất nhanh (đặc biệt là mảng Cloud kết hợp AI). Không chỉ giúp tích lũy kiến thức để hướng tới các chứng chỉ AWS, chương trình còn rèn luyện thói quen viết tài liệu kỹ thuật, chia sẻ cộng đồng và tư duy kiến trúc bài bản — rất hữu ích cho bất kỳ sinh viên CNTT/AI nào chuẩn bị bước vào ngành.

  Với bạn mới học Cloud, mình sẽ khuyên học theo thứ tự, tự làm lại các bước chính của bài lab và ghi lại một điều hiểu được sau mỗi buổi. Với bạn quan tâm AI, dự án nhóm là dịp để thử đưa mô hình vào một luồng xử lý có lưu trữ, hàng đợi và giám sát.

### Đề xuất & mong muốn

- Khối lượng kiến thức và bài lab trong lộ trình khá dày ở các tuần giữa; nếu có thêm tài liệu tóm tắt nhanh (cheat-sheet) các lỗi cấu hình thường gặp về `IAM` và `VPC` theo từng module sẽ giúp các bạn mới làm quen AWS tiết kiệm thời gian gỡ lỗi hơn.
- Có thể tăng thêm thời lượng cho các phiên thực hành ngắn (**Hands-on mini challenge**) trong các buổi offline để người tham dự có thêm thời gian trao đổi trực tiếp với mentor ngay tại chỗ.
- Mình mong có thêm một buổi thực hành theo nhóm đi qua toàn bộ luồng từ lúc nộp dữ liệu, đưa công việc vào hàng đợi, chạy bộ chấm AI đến lúc xem kết quả và log. Cuối buổi, mỗi nhóm có thể trình bày một quyết định thiết kế và một lỗi đã gặp để cùng trao đổi cách xử lý.
