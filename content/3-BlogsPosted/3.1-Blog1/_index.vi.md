---
title: "Blog 1 - AWS CLI và AWS MCP Server trong thời đại Vibe Coding"
date: 2026-11-19
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

{{% notice info %}}
🔗 **Bài đăng trên AWS Study Group:** [Xem bài viết Facebook](https://www.facebook.com/share/p/19vbHFir6p/)
{{% /notice %}}

**AWS CLI TRONG THỜI ĐẠI VIBE CODING: TỪ GÕ LỆNH THỦ CÔNG ĐẾN AWS MCP SERVER**

Trước đây, kỹ sư làm việc với AWS thường mở terminal lên và tự gõ từng dòng lệnh `aws ...`. Sang thời đại Vibe Coding — khi nhiều người dùng AI coding agent (Claude Code, Cursor, Kiro...) để dựng hệ thống bằng câu lệnh tự nhiên — cách chúng ta dùng dòng lệnh để tương tác với AWS cũng đang thay đổi rất nhanh.

**1. AWS CLI là gì và vì sao vẫn quan trọng?**

**AWS Command Line Interface (AWS CLI)** là công cụ mã nguồn mở (open-source) của AWS, cho phép bạn tương tác và quản lý các dịch vụ AWS trực tiếp từ terminal (Linux/macOS shell, Windows CMD/PowerShell hoặc chạy từ xa trên EC2/Systems Manager).

Dù nhiều người quen thao tác trên trình duyệt, `AWS CLI` vẫn luôn là công cụ cốt lõi vì 3 điểm mạnh:
* **Tương đương AWS Management Console:** Mọi thao tác quản trị, cấu hình IaaS có trên Console đều có thể thực hiện qua CLI (các dịch vụ/tính năng mới thường hỗ trợ đầy đủ ngay khi ra mắt hoặc trong vòng 180 ngày).
* **Gọi trực tiếp Public AWS APIs:** Giúp kiểm tra tài nguyên nhanh, chuẩn xác mà không cần bấm qua nhiều màn hình.
* **Tự động hóa bằng script:** Dễ dàng ghép các lệnh vào shell script hoặc CI/CD pipeline để xử lý các tác vụ lặp lại.

**2. 3 "bẫy" hay gặp khi để AI tự viết lệnh AWS CLI (Vibe Coding)**

Khi chuyển sang Vibe Coding, nhiều người chỉ cần mô tả yêu cầu rồi để AI tự sinh và chạy lệnh `AWS CLI`. Nhưng thực tế lại phát sinh 3 vấn đề lớn:
* **Dùng kiến thức cũ:** LLM bị giới hạn bởi knowledge cutoff nên không biết các dịch vụ hoặc tính năng mới (ví dụ Amazon S3 Vectors, Amazon Aurora DSQL, Amazon Bedrock AgentCore) và dễ đoán sai cú pháp/flag của `AWS CLI`.
* **Lạm dụng `AWS CLI` thay cho IaC:** Khi được nhờ dựng hạ tầng, AI hay tạo một loạt lệnh `AWS CLI` rời rạc thay vì dùng công cụ Infrastructure as Code chuẩn như **AWS CDK** hay **AWS CloudFormation**.
* **Cấp quyền `IAM` quá rộng:** Các script AI viết ra thường gắn permission dư thừa để "chạy được ngay", dùng thử thì tiện nhưng tiềm ẩn rủi ro lớn nếu đưa lên production.

**3. Bước tiến mới: AWS MCP Server (thuộc Agent Toolkit for AWS)**

Thay vì để AI tự đoán mò lệnh CLI từ trí nhớ, AWS đã phát hành chính thức (**General Availability** từ tháng 5/2026) **AWS MCP Server** — một remote MCP server do AWS quản lý, kết nối an toàn AI coding agent với AWS API thông qua bộ tool gọn nhẹ (không làm phình context window):
* **`search_documentation` & `read_documentation`:** Tra cứu tài liệu và best practices mới nhất của AWS ngay tại thời điểm hỏi (không cần xác thực, không phụ thuộc dữ liệu huấn luyện cũ).
* **`call_aws`:** Thực thi hơn 15.000 AWS API operations bằng chính IAM credentials của bạn (API mới ra mắt sẽ được hỗ trợ trong vài ngày).
* **`run_script`:** Cho phép AI viết một đoạn Python ngắn chạy trong sandbox phía server (kế thừa quyền IAM của bạn nhưng **không có truy cập mạng**, **không chạm vào local filesystem hay shell**) để gom nhiều API call và lọc dữ liệu chỉ trong 1 round-trip.
* **Skills:** Bộ hướng dẫn chuẩn do chính các team dịch vụ AWS duy trì, giúp AI đi đúng best practices và giảm hallucination.

**4. Kiểm soát an toàn & Lưu ý thực tế**

Để đưa AI vào quy trình làm việc mà vẫn giữ an toàn hệ thống:
* **Xác thực chuẩn IAM SigV4:** Kết nối từ máy local thông qua proxy mã nguồn mở `mcp-proxy-for-aws` (cầu nối giữa OAuth 2.1 của MCP và IAM SigV4).
* **Tách quyền người vs agent:** Dùng **IAM Policy** hoặc **Service Control Policy (SCP)** để giới hạn: người dùng có quyền thay đổi tài nguyên, còn agent qua MCP Server chỉ được quyền **read-only**.
* **Giám sát & Audit rõ ràng:** Metric gọi từ MCP Server được ghi riêng trên **Amazon CloudWatch** (namespace `AWS-MCP`) và toàn bộ lịch sử API call vẫn được lưu đầy đủ trên **Amazon CloudTrail**.
* **Chi phí & Region:** AWS không thu thêm phí cho riêng AWS MCP Server (chỉ tính phí tài nguyên AWS bạn tạo ra và data transfer); endpoint đặt tại `us-east-1` (N. Virginia) và `eu-central-1` (Frankfurt), có thể gọi API tới mọi Region.

**Tóm lại:** `AWS CLI` vẫn cực kỳ giá trị cho thao tác nhanh và automation script. Nhưng trong thời đại Vibe Coding, hãy dùng IaC cho hạ tầng chính và kết nối AI qua **AWS MCP Server** kèm rào chắn **IAM** thay vì copy-paste lệnh CLI theo cảm tính.

**Nguồn tham khảo:**
* What is the AWS Command Line Interface? — AWS Documentation (https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)
* The AWS MCP Server is now generally available — AWS News Blog (https://aws.amazon.com/blogs/aws/the-aws-mcp-server-is-now-generally-available/)
* **Nguồn ảnh:** AWS News Blog — *The AWS MCP Server is now generally available* (https://d2908q01vomqb2.cloudfront.net/da4b9237bacccdf19c0760cab7aec4a8359010b0/2026/05/06/agent-toolkit-4-1-1260x625.png)
