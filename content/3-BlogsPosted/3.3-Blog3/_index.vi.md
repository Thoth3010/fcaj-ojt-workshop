---
title: "Blog 3 - Amazon Bedrock AgentCore Harness"
date: 2026-11-23
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

{{% notice info %}}
🔗 **Bài đăng trên AWS Study Group:** [Xem bài viết Facebook](https://www.facebook.com/share/p/19vbHFir6p/)
{{% /notice %}}

# Agent Harness của AWS là gì? Cách Amazon Bedrock AgentCore Harness đưa AI Agent từ Demo lên Production

Tạo một AI Agent chạy trên laptop không còn quá khó. Thách thức xuất hiện khi đưa agent lên production cho nhiều người dùng: model cần sandbox, memory, tool/MCP, identity, concurrency, log, trace và cơ chế kiểm soát hành động rủi ro. Lớp điều phối bao quanh model đó được gọi là Agent Harness.

![Kiến trúc Amazon Bedrock AgentCore Harness](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2026/06/11/ML-20804-1.png)

## 1. Agent Harness là gì?

Một AI Agent thường là LLM gọi tool trong một vòng lặp để hoàn thành mục tiêu. Phần khó trong production không chỉ là vòng lặp, mà là kết nối an toàn với:

- Sandbox chạy lệnh và code.
- Bộ nhớ xuyên phiên.
- Tool, skills và MCP server.
- Identity và phân quyền.
- Concurrency và lưu trữ phiên.
- Log, trace, evaluation và kiểm soát rủi ro.

Agent Harness là lớp khung điều phối và hạ tầng vận hành bao quanh model, biến những thành phần rời thành một nền tảng có thể cấu hình và mở rộng.

## 2. Amazon Bedrock AgentCore Harness

Amazon Bedrock AgentCore Harness đóng gói năng lực production thông qua CreateHarness và InvokeHarness, với các nhóm cấu hình chính:

### Models

Harness hỗ trợ model trên Amazon Bedrock và các provider bên ngoài. Hệ thống có thể chuyển model giữa phiên mà vẫn giữ context; API key bên ngoài được lưu trong AgentCore Identity token vault.

### Tools và Skills

Có thể khai báo AgentCore Gateway, remote MCP, AgentCore Browser, Code Interpreter và inline function cho human-in-the-loop. Skills có thể được nạp từ AWS Skills, Git repository, Amazon S3 hoặc container.

### Memory và runtime cô lập

Managed memory hỗ trợ semantic retrieval và summarization, tách dữ liệu theo actorId. Mỗi phiên chạy trong Firecracker microVM cô lập và có thể dùng managed session storage, Amazon EFS hoặc Amazon S3 Files.

### Observability, evaluation và export

Trace và log được đưa vào CloudWatch GenAI Observability. AgentCore Evaluations hỗ trợ đánh giá chất lượng, còn endpoint versioning giúp quản lý staging, production và rollback. Khi cần tùy biến sâu hơn, harness có thể được export thành Strands code.

## 3. Strands Harness defaults và Lifecycle Hooks

Các bản cập nhật mới bổ sung:

- Prompt caching, conversation summarization và context offloading để giảm lượng token phải giữ trong context.
- Built-in tools như todo_write, subagent, web_fetch cùng quyền read, write và edit tách biệt.
- Bốn lifecycle hook: before_invocation, before_tool_call, after_tool_call và after_invocation.

Lifecycle hook cho phép chèn kiểm tra tất định. Ví dụ, Lambda tại before_tool_call có thể chặn giao dịch hoàn tiền vượt hạn mức; failureMode mặc định là deny nếu bước kiểm tra lỗi hoặc timeout. Hook cũng có thể gửi sự kiện bất đồng bộ qua Amazon SNS hoặc Amazon EventBridge.

## 4. Chi phí và kiểm soát quyền

- Harness không có phí riêng; chi phí đến từ các thành phần bên dưới và mức tài nguyên sử dụng.
- AgentCore Runtime tính compute theo CPU và bộ nhớ thực sự tiêu thụ; giá phụ thuộc Region.
- Nếu allowedTools để trống hoặc dùng wildcard, harness có thể nhận thêm built-in tools trong tương lai. Ứng dụng cần phạm vi cố định nên liệt kê tool cụ thể và dùng before_tool_call hook cho hành động rủi ro.

## Kết luận

Khoảng cách giữa một AI Agent demo và hệ thống production nằm ở Agent Harness. Amazon Bedrock AgentCore Harness kết hợp runtime cô lập, managed memory, tools, observability, evaluation và lifecycle hooks để kiểm soát độ tin cậy, bảo mật và chi phí mà không phải tự xây toàn bộ lớp điều phối.

## Nguồn tham khảo

- [Amazon Bedrock AgentCore harness is now generally available — AWS AI Blog](https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-agentcore-harness-is-now-generally-available-go-from-idea-to-production-grade-agent-in-minutes/)
- [AgentCore harness adds Strands defaults, built-in tools, and lifecycle hooks — AWS AI Blog](https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-agentcore-harness-adds-strands-harness-defaults-built-in-tools-and-lifecycle-hooks/)
- [Nguồn ảnh — AWS AI Blog](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2026/06/11/ML-20804-1.png)
