---
title: "Blog 1 - AWS CLI và AWS MCP Server trong thời đại Vibe Coding"
date: 2026-11-19
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

{{% notice info %}}
🔗 **Bài đăng trên AWS Study Group:** [Xem bài viết Facebook](https://www.facebook.com/share/p/1FJJYqU4Rp/)
{{% /notice %}}

# AWS CLI trong thời đại Vibe Coding: Từ gõ lệnh thủ công đến AWS MCP Server

Trước đây, kỹ sư làm việc với AWS thường mở terminal và tự gõ từng lệnh aws. Trong thời đại Vibe Coding, nhiều người dùng AI coding agent như Claude Code, Cursor hoặc Kiro để dựng hệ thống bằng ngôn ngữ tự nhiên. Vì vậy, cách chúng ta dùng dòng lệnh để tương tác với AWS cũng đang thay đổi.

![Agent Toolkit for AWS và AWS MCP Server](https://d2908q01vomqb2.cloudfront.net/da4b9237bacccdf19c0760cab7aec4a8359010b0/2026/05/06/agent-toolkit-4-1-1260x625.png)

## 1. AWS CLI là gì và vì sao vẫn quan trọng?

AWS Command Line Interface là công cụ mã nguồn mở cho phép quản lý dịch vụ AWS trực tiếp từ Linux/macOS shell, Windows CMD/PowerShell hoặc từ xa trên EC2 và Systems Manager.

AWS CLI vẫn là công cụ cốt lõi vì:

- Có thể thực hiện hầu hết thao tác quản trị và cấu hình tương đương AWS Management Console.
- Gọi trực tiếp AWS public APIs, giúp kiểm tra tài nguyên nhanh và chính xác.
- Dễ ghép lệnh vào shell script hoặc CI/CD pipeline để tự động hóa tác vụ lặp lại.

## 2. Ba bẫy khi để AI tự viết lệnh AWS CLI

### Dùng kiến thức cũ

LLM bị giới hạn bởi knowledge cutoff nên có thể không biết dịch vụ hoặc tính năng mới, dẫn đến đoán sai command, flag hoặc cấu trúc API.

### Lạm dụng AWS CLI thay cho Infrastructure as Code

Khi được yêu cầu dựng hạ tầng, AI thường sinh một chuỗi lệnh rời rạc. Cách này chạy nhanh khi demo nhưng khó review, lặp lại, rollback và quản lý vòng đời hơn AWS CDK hoặc AWS CloudFormation.

### Cấp quyền IAM quá rộng

Script do AI sinh có thể gắn permission dư thừa để “chạy được ngay”. Điều này tiện khi thử nghiệm nhưng tạo rủi ro lớn nếu áp dụng vào production.

## 3. AWS MCP Server và Agent Toolkit for AWS

AWS MCP Server là remote MCP server do AWS quản lý, giúp AI coding agent làm việc với AWS bằng các tool nhỏ gọn thay vì tự đoán lệnh từ trí nhớ:

- **search_documentation và read_documentation:** tra cứu tài liệu và best practices mới nhất.
- **call_aws:** gọi các AWS API operation bằng IAM credentials hiện tại.
- **run_script:** chạy Python trong sandbox phía server để gom nhiều API call và lọc kết quả trong một round trip; sandbox không truy cập mạng, local filesystem hoặc shell.
- **Skills:** hướng dẫn do các team dịch vụ AWS duy trì để agent tuân thủ best practices và giảm hallucination.

## 4. Kiểm soát an toàn

- Dùng IAM SigV4 và mcp-proxy-for-aws để kết nối an toàn từ môi trường local.
- Tách quyền người dùng và agent bằng IAM Policy hoặc Service Control Policy; có thể cho agent quyền read-only.
- Theo dõi metric của MCP Server trong Amazon CloudWatch và lịch sử API call trong AWS CloudTrail.
- AWS không thu phí riêng cho AWS MCP Server; chi phí vẫn đến từ tài nguyên AWS và data transfer phát sinh.

## Kết luận

AWS CLI vẫn rất hữu ích cho thao tác nhanh và automation script. Tuy nhiên, hạ tầng chính nên được quản lý bằng IaC, còn AI agent nên kết nối với AWS qua MCP Server cùng rào chắn IAM rõ ràng thay vì tự sinh và chạy lệnh theo cảm tính.

## Nguồn tham khảo

- [What is the AWS Command Line Interface? — AWS Documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)
- [The AWS MCP Server is now generally available — AWS News Blog](https://aws.amazon.com/blogs/aws/the-aws-mcp-server-is-now-generally-available/)
- [Nguồn ảnh — AWS News Blog](https://d2908q01vomqb2.cloudfront.net/da4b9237bacccdf19c0760cab7aec4a8359010b0/2026/05/06/agent-toolkit-4-1-1260x625.png)
