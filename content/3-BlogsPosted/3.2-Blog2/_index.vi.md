---
title: "Blog 2 - Infrastructure as Code và AWS IaC MCP Server"
date: 2026-11-20
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

{{% notice info %}}
🔗 **Bài đăng trên AWS Study Group:** [Xem bài viết Facebook](https://www.facebook.com/share/p/1BYTn5tpyW/)
{{% /notice %}}

# Vibe Coding hạ tầng AWS: Tại sao cần Infrastructure as Code và AWS IaC MCP Server?

AI giúp viết code ứng dụng rất nhanh. Tuy nhiên, nếu để AI dựng hạ tầng AWS bằng những lệnh rời rạc, hệ thống có thể chạy được ở bản demo nhưng khó kiểm soát khi đưa lên production. Vì vậy, Vibe Coder cần hiểu Infrastructure as Code và các công cụ AWS hỗ trợ quy trình này.

![Quy trình AWS IaC MCP Server](https://d2908q01vomqb2.cloudfront.net/7719a1c782a1ba91c031a682a0a2f8658209adbf/2026/08/04/figure1-iac-mcp-workflow.png)

## 1. Infrastructure as Code trên AWS

Infrastructure as Code cho phép định nghĩa tài nguyên AWS trong file code để triển khai đồng nhất, lặp lại được và dễ kiểm soát tuân thủ.

Hai công cụ IaC gốc phổ biến trên AWS là:

- **AWS CloudFormation:** khai báo hạ tầng bằng template JSON hoặc YAML.
- **AWS Cloud Development Kit:** viết hạ tầng bằng TypeScript, Python và các ngôn ngữ quen thuộc, sau đó tổng hợp thành CloudFormation.

Với Vibe Coding, yêu cầu AI tạo CloudFormation hoặc AWS CDK giúp thay đổi được review trên Git và quản lý vòng đời bài bản hơn một chuỗi AWS CLI command.

## 2. Ba điểm nghẽn khi AI tự viết CloudFormation hoặc CDK

### Dữ liệu cũ hoặc sai thuộc tính

Nếu không tra cứu tài liệu live, AI có thể dùng sai property hoặc bỏ qua best practices mới.

### Chuyển đổi qua nhiều công cụ

Kỹ sư phải liên tục chuyển giữa documentation, linter, console triển khai và log chỉ để hoàn thành một vòng viết, kiểm tra và deploy.

### Khó tìm nguyên nhân deploy thất bại

CloudFormation stack có thể báo AccessDenied hoặc ROLLBACK_COMPLETE nhưng stack events chưa chỉ rõ permission còn thiếu. Người vận hành phải đối chiếu thêm AWS CloudTrail.

## 3. AWS Infrastructure as Code MCP Server

AWS IaC MCP Server chạy cục bộ qua stdio và hỗ trợ các AI assistant tương thích MCP. Công cụ này khép kín quy trình bốn bước:

### Author

Các tool tìm kiếm CloudFormation/CDK documentation, sample và construct giúp agent lấy đúng schema và best practices trước khi sinh code.

### Validate

- **validate_cloudformation_template** dùng cfn-lint để kiểm tra cấu trúc và schema.
- **check_cloudformation_template_compliance** dùng cfn-guard để kiểm tra yêu cầu như mã hóa S3, Block Public Access hoặc log retention.

Hai bước này chạy local và chưa cần quyền AWS.

### Deploy

Template đã kiểm tra được triển khai qua AWS CLI. Pre-deployment validation có thể được cấu hình trước khi tạo change set.

### Troubleshoot

**troubleshoot_cloudformation_deployment** kết hợp stack events với AWS CloudTrail để xác định permission còn thiếu, chẳng hạn iam:PassRole khi gắn role cho Lambda.

## 4. Lưu ý an toàn

- Các bước validate không cần quyền AWS; troubleshoot chỉ cần quyền đọc CloudFormation và CloudTrail.
- Dữ liệu trả về cho AI model provider phải tuân thủ quy định bảo mật của tổ chức.
- CloudTrail có thể cần 5–15 phút để hiển thị event sau một deployment lỗi.

## Kết luận

Để Vibe Code hạ tầng AWS nhanh nhưng vẫn sẵn sàng cho production, nên yêu cầu AI tạo CloudFormation hoặc AWS CDK và dùng AWS IaC MCP Server cho vòng lặp Author → Validate → Deploy → Troubleshoot.

## Nguồn tham khảo

- [Accelerate CloudFormation development with the IaC MCP Server — AWS DevOps Blog](https://aws.amazon.com/blogs/devops/accelerate-cloudformation-development-with-the-iac-mcp-server/)
- [Introducing the AWS Infrastructure as Code MCP Server — AWS DevOps Blog](https://aws.amazon.com/blogs/devops/introducing-the-aws-infrastructure-as-code-mcp-server-ai-powered-cdk-and-cloudformation-assistance/)
- [Nguồn ảnh — AWS DevOps Blog](https://d2908q01vomqb2.cloudfront.net/7719a1c782a1ba91c031a682a0a2f8658209adbf/2026/08/04/figure1-iac-mcp-workflow.png)
