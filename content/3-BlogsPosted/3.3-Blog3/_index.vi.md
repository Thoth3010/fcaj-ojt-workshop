---
title: "Blog 3 - Amazon Bedrock AgentCore Harness"
date: 2026-11-23
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

{{% notice info %}}
🔗 **Bài đăng trên AWS Study Group:** [Xem bài viết Facebook](https://www.facebook.com/share/p/1FJJYqU4Rp/)
{{% /notice %}}

**AGENT HARNESS CỦA AWS LÀ GÌ? CÁCH AMAZON BEDROCK AGENTCORE HARNESS ĐƯA AI AGENT TỪ DEMO LÊN PRODUCTION**

Tự vibe code ra một AI Agent chạy được trên laptop trong một buổi chiều bây giờ không còn khó. Nhưng khi muốn đưa nó lên production phục vụ nhiều người dùng thật, nút thắt thường không nằm ở model thông minh tới đâu — mà nằm ở lớp hạ tầng và điều phối bao quanh nó, thứ gọi là **Agent Harness**.

**1. Agent Harness là gì và tại sao AI Agent không thể chỉ có LLM?**

Về bản chất, một AI Agent là LLM chạy các tool trong một vòng lặp để hoàn thành mục tiêu (Kiro, Claude Code hay Codex đều vận hành theo cấu trúc này). Nhưng vòng lặp không phải phần khó nhất — phần khiến team tốn hàng tấn thời gian là kết nối AI agent với mọi thứ xung quanh: sandbox chạy lệnh/code an toàn, bộ nhớ xuyên phiên, kết nối tool/MCP, phân quyền identity, concurrency, quan sát log/trace và kiểm soát hành vi rủi ro.

**Agent Harness** chính là lớp khung điều phối + hạ tầng vận hành bao quanh model, biến việc "tự nối dây từng mảnh" thành một nền tảng có thể cấu hình và chạy thẳng ở quy mô production.

**2. Kiến trúc Amazon Bedrock AgentCore Harness có gì bên trong?**

Thay vì phải tự dựng container, nối runtime, memory hay observability bằng tay, **Amazon Bedrock AgentCore harness** (đạt General Availability từ 06/2026) đóng gói toàn bộ năng lực production sau đúng **2 API chính: `CreateHarness` và `InvokeHarness`**, gồm 4 lớp cấu hình chính chạy trên hạ tầng cô lập (như sơ đồ đính kèm):
* **Models (Đổi model linh hoạt):** Dùng model trên Amazon Bedrock, gọi trực tiếp OpenAI/Gemini hoặc qua LiteLLM — đặc biệt có thể **đổi provider ngay giữa phiên mà không mất context** (ví dụ lập kế hoạch bằng một model rồi chuyển sang model khác để viết code). API key của provider ngoài được lưu an toàn trong AgentCore Identity token vault.
* **Tools & Skills theo kiểu khai báo:** Gắn sẵn `AgentCore Gateway`, `remote_mcp`, `AgentCore Browser`, `AgentCore Code Interpreter`, `inline_function` (cho bước human-in-the-loop), kèm sẵn shell và thao tác file. Hỗ trợ nạp **Skills** theo yêu cầu từ `awsSkills`, Git repo, Amazon S3 hoặc container.
* **Memory & Runtime cô lập:** Tự động cấp phát managed memory (chiến lược `SEMANTIC` + `SUMMARIZATION`, lưu sự kiện mặc định 30 ngày, tách riêng từng người dùng theo `actorId`). Mỗi phiên chạy trong **Firecracker microVM** cô lập, hỗ trợ lưu trữ phiên (managed session storage) hoặc gắn **Amazon EFS** / **Amazon S3 Files**.
* **Observability, Evaluation & Export ra code:** Gom toàn bộ trace/log vào **CloudWatch GenAI Observability** (tab Harnesses), chấm điểm chất lượng tự động bằng **AgentCore Evaluations**, quản lý version/rollback theo endpoint (`PROD`, `STAGING`). Khi hệ thống cần tùy biến vượt ngoài cấu hình, một lệnh `agentcore export harness` sẽ xuất thẳng thành code **Strands** để phát triển tiếp mà không phải làm lại từ đầu.

**3. Bản nâng cấp mới nhất (11/2026): Strands Harness Defaults & Lifecycle Hooks**

Tháng 11/2026, AWS tiếp tục nâng cấp AgentCore harness sử dụng nền tảng mã nguồn mở **Strands harness** (Apache 2.0) làm mặc định kèm 2 bổ sung rất giá trị cho hệ thống thật:
* **Tối ưu context & bổ sung built-in tools:** Tích hợp prompt caching tự động (khởi đầu cho model Anthropic trên Bedrock), chủ động tóm tắt hội thoại cũ (AWS ghi nhận giúp **giảm khoảng 34% chi phí token** so với các harness hàng đầu khác), context offloading cho kết quả tool lớn, cùng các tool built-in mới như `todo_write` (giữ kế hoạch xuyên phiên), `subagent` (ủy thác tác vụ con), `web_fetch` và phân quyền file tách biệt (`read`, `write`, `edit`).
* **Lifecycle Hooks (Kiểm soát hành vi bằng code tất định):** Cho phép chèn logic kiểm tra tại 4 mốc trong vòng lặp: `before_invocation`, `before_tool_call`, `after_tool_call`, `after_invocation`. Ví dụ: gắn một **AWS Lambda** ở `before_tool_call` để chặn tự động mọi lệnh hoàn tiền vượt hạn mức (áp dụng cho cả `subagent`; nếu Lambda lỗi hoặc timeout, `failureMode` mặc định là `deny`), hoặc gửi thông báo bất đồng bộ sang **Amazon SNS / Amazon EventBridge**.

**4. Chi phí & Lưu ý thực tế khi áp dụng**

* **Không thu thêm phí riêng cho Harness:** Bạn chỉ trả tiền theo mức dùng thực tế của các thành phần bên dưới. Theo công bố GA của AWS, compute trên **AgentCore Runtime** tính theo CPU tiêu thụ chủ động từng giây (`$0.0895 / vCPU-hour`, `$0.00945 / GB-hour` — không tính phí CPU khi agent đang chờ model hoặc tool I/O; mức giá thực tế phụ thuộc Region và tài nguyên sử dụng).
* **Khóa chặt `allowedTools` khi cần ranh giới cố định:** Nếu bỏ trống `allowedTools` hoặc đặt `["*"]`, harness sẽ tự động hưởng các built-in tool mới AWS bổ sung theo thời gian. Với ứng dụng yêu cầu phạm vi quyền cố định, hãy liệt kê tường minh tool được phép (ví dụ `["read", "web_fetch"]`) và kết hợp **Lambda `before_tool_call` hook** cho mọi hành động có rủi ro cao.

**Tóm lại:** Trong kỷ nguyên Vibe Coding và Agentic AI, khoảng cách giữa một bản demo vui và một AI Agent chạy được trên production nằm ở **Agent Harness**. Kết hợp **Amazon Bedrock AgentCore harness**, **Strands harness** và **Lifecycle Hooks** giúp đội ngũ kỹ sư kiểm soát được cả độ tin cậy, bảo mật lẫn chi phí mà không phải tự viết lại toàn bộ hạ tầng điều phối.

**Nguồn tham khảo:**
* Amazon Bedrock AgentCore harness is now generally available: Go from idea to production-grade agent in minutes — AWS Artificial Intelligence Blog (https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-agentcore-harness-is-now-generally-available-go-from-idea-to-production-grade-agent-in-minutes/)
* Amazon Bedrock AgentCore harness adds Strands harness defaults, built-in tools, and lifecycle hooks — AWS Artificial Intelligence Blog (https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-agentcore-harness-adds-strands-harness-defaults-built-in-tools-and-lifecycle-hooks/)
* **Nguồn ảnh:** AWS Artificial Intelligence Blog — *Amazon Bedrock AgentCore harness is now generally available* (https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2026/06/11/ML-20804-1.png)
