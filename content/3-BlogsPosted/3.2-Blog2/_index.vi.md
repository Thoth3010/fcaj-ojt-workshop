---
title: "Blog 2 - Infrastructure as Code và AWS IaC MCP Server"
date: 2026-11-20
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

**VIBE CODING HẠ TẦNG AWS: TẠI SAO CẦN INFRASTRUCTURE AS CODE & AWS IaC MCP SERVER?**

Ở bài trước mình có nói về `AWS CLI` trong thời đại Vibe Coding. Sang bước tiếp theo, AI giúp viết code ứng dụng cực nhanh, nhưng khi nhờ AI dựng luôn hạ tầng AWS bằng các lệnh rời rạc thì rất dễ rơi vào cảnh "chạy được lúc demo, khó kiểm soát lúc lên production". Vậy Vibe Coder cần nắm nền tảng gì và AWS đã chuẩn bị công cụ nào cho bài toán hạ tầng?

**1. Kiến thức nền cho Vibe Coder: Infrastructure as Code (IaC) trên AWS là gì?**

Thay vì bấm tay trên Console hay chạy từng dòng `AWS CLI` rời rạc, **Infrastructure as Code (IaC)** cho phép định nghĩa toàn bộ tài nguyên AWS dưới dạng file code để triển khai đồng nhất, lặp lại được và dễ kiểm soát tuân thủ. Trên AWS có 2 công cụ IaC gốc phổ biến nhất:
* **AWS CloudFormation:** Khai báo hạ tầng dưới dạng template JSON/YAML.
* **AWS Cloud Development Kit (AWS CDK):** Viết hạ tầng bằng ngôn ngữ lập trình quen thuộc (như TypeScript, Python...) rồi biên dịch ra CloudFormation.

Với Vibe Coder, yêu cầu AI xuất ra template **CloudFormation** hoặc **AWS CDK** thay vì câu lệnh rời giúp bạn dễ review trên Git, kiểm soát thay đổi và quản lý vòng đời tài nguyên bài bản hơn.

**2. 3 điểm nghẽn khi Vibe Coder để AI tự viết CloudFormation / CDK**

Theo ghi nhận từ đội ngũ AWS DevOps, nếu chỉ dùng AI thuần theo kiểu chat thông thường, quy trình làm IaC rất dễ vướng 3 điểm nghẽn:
* **Dữ liệu cũ, sai thuộc tính tài nguyên:** Không tra cứu tài liệu live khiến AI dễ đoán nhầm tên property hoặc bỏ qua best practices mới.
* **Chuyển đổi qua lại quá nhiều công cụ:** Kỹ sư phải nhảy liên tục giữa trang tài liệu, linter, console triển khai và log chỉ cho một vòng lặp viết – kiểm tra – deploy.
* **Mò lỗi triển khai mất thời gian:** Khi CloudFormation stack báo lỗi như `AccessDenied` hoặc rơi vào trạng thái `ROLLBACK_COMPLETE`, stack event nhiều khi không chỉ rõ thiếu permission gì — buộc bạn phải tự mở **AWS CloudTrail** đối chiếu từng API call.

**3. AWS chuẩn bị gì cho kỷ nguyên Vibe Coding? — AWS IaC MCP Server**

Để giải quyết đúng các điểm nghẽn trên, AWS đã phát hành **AWS Infrastructure as Code (IaC) MCP Server** (`awslabs.aws-iac-mcp-server`) chạy cục bộ qua `uv` (giao tiếp `stdio`, không mở port mạng) cho các AI assistant hỗ trợ MCP như **Kiro**, **Kiro CLI**, **Claude** hay **Cursor**.

Theo đúng quy trình **4 bước (`Author → Validate → Deploy → Troubleshoot`)** trên sơ đồ đính kèm, server này cung cấp 9 tool chuyên biệt:
* **Step 1 — Author (Tra docs & viết template chuẩn):** Dùng các tool kết nối AWS Knowledge MCP backend (`search_cloudformation_documentation`, `search_cdk_documentation`, `search_cdk_samples_and_constructs`, `read_iac_documentation_page`) cùng `cdk_best_practices` để lấy đúng cú pháp tài nguyên và mẫu chuẩn trước khi sinh code.
* **Step 2 — Validate (Bắt lỗi cú pháp & bảo mật ngay tại máy):** Dùng `validate_cloudformation_template` (bọc `cfn-lint` kiểm tra cấu trúc/schema) và `check_cloudformation_template_compliance` (bọc `cfn-guard` kiểm tra bảo mật như mã hóa S3, Block Public Access, log retention). Bước này chạy hoàn toàn local, chưa cần quyền AWS.
* **Step 3 — Deploy:** Triển khai template đã kiểm tra qua `AWS CLI` (ngoài ra có tool `get_cloudformation_pre_deploy_validation_instructions` hỗ trợ cấu hình kiểm tra trước khi tạo change set).
* **Step 4 — Troubleshoot (Chẩn đoán lỗi bằng CloudTrail):** Khi deploy thất bại, tool `troubleshoot_cloudformation_deployment` tự lấy stack events đối chiếu với **AWS CloudTrail** để chỉ ra chính xác permission còn thiếu (ví dụ thiếu `iam:PassRole` khi gắn role cho Lambda).

**4. Lưu ý an toàn & thói quen thực tế cho Vibe Coder**

* **Phân quyền tối thiểu (Least Privilege):** Các tool validate/compliance không cần quyền AWS; còn khi troubleshoot, chỉ cần cấp quyền **read-only** (`cloudformation:DescribeStacks`, `DescribeStackEvents`, `DescribeStackResources`, `cloudtrail:LookupEvents`).
* **Lưu ý bảo mật dữ liệu:** Server chạy local qua `stdio` (chỉ kết nối ngoài khi tra documentation), nhưng dữ liệu phản hồi khi troubleshoot sẽ đi qua AI model provider bạn dùng (Kiro, Claude, Cursor...) — hãy đảm bảo tuân thủ quy định bảo mật của tổ chức.
* **Mẹo khi troubleshoot:** Sự kiện trên **CloudTrail** thường mất khoảng **5–15 phút** mới xuất hiện sau lúc deploy lỗi, nên hãy đợi ít nhất 5 phút trước khi chạy bước troubleshoot để phân tích đầy đủ nhất.

**Tóm lại:** Muốn vibe code hạ tầng AWS nhanh mà vẫn chuẩn production, hãy yêu cầu AI tạo **CloudFormation / AWS CDK** kết hợp **AWS IaC MCP Server** để khép kín vòng lặp tra docs mới → check cú pháp & bảo mật tại máy → deploy → tìm nguyên nhân lỗi ngay trong một khung chat.

**Nguồn tham khảo:**
* Accelerate CloudFormation development with the IaC MCP Server — AWS DevOps & Developer Productivity Blog (https://aws.amazon.com/blogs/devops/accelerate-cloudformation-development-with-the-iac-mcp-server/)
* Introducing the AWS Infrastructure as Code MCP Server: AI-Powered CDK and CloudFormation Assistance — AWS DevOps & Developer Productivity Blog (https://aws.amazon.com/blogs/devops/introducing-the-aws-infrastructure-as-code-mcp-server-ai-powered-cdk-and-cloudformation-assistance/)
* **Nguồn ảnh:** AWS DevOps & Developer Productivity Blog — *Accelerate CloudFormation development with the IaC MCP Server* (https://d2908q01vomqb2.cloudfront.net/7719a1c782a1ba91c031a682a0a2f8658209adbf/2026/08/04/figure1-iac-mcp-workflow.png)
