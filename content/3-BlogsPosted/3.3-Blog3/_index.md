---
title: "Blog 3 - Amazon Bedrock AgentCore Harness"
date: 2026-11-23
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

{{% notice info %}}
🔗 **AWS Study Group post:** [View the Facebook post](https://www.facebook.com/share/p/19vbHFir6p/)
{{% /notice %}}

# What Is an AWS Agent Harness? Taking AI Agents from Demo to Production with Amazon Bedrock AgentCore

Building an AI agent that runs on a laptop is no longer especially difficult. Production introduces the real challenge: the model needs a sandbox, memory, tools and MCP connections, identity, concurrency controls, logs, traces, and deterministic checks around risky actions. The orchestration layer around the model is the Agent Harness.

![Amazon Bedrock AgentCore Harness architecture](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2026/06/11/ML-20804-1.png)

## 1. What is an Agent Harness?

An AI agent is typically an LLM calling tools in a loop to achieve a goal. Production complexity comes from connecting that loop safely to:

- Sandboxed command and code execution.
- Cross-session memory.
- Tools, skills, and MCP servers.
- Identity and authorization.
- Concurrency and session storage.
- Logs, traces, evaluations, and risk controls.

An Agent Harness is the orchestration and operational layer that turns those separate pieces into a configurable, scalable platform.

## 2. Amazon Bedrock AgentCore Harness

Amazon Bedrock AgentCore Harness packages production capabilities behind CreateHarness and InvokeHarness.

### Models

The harness supports models on Amazon Bedrock and external providers. A session can switch models without losing context, while external provider keys are stored in the AgentCore Identity token vault.

### Tools and Skills

Configuration can attach AgentCore Gateway, remote MCP servers, AgentCore Browser, Code Interpreter, and inline functions for human-in-the-loop steps. Skills can be loaded from AWS Skills, Git repositories, Amazon S3, or containers.

### Memory and isolated runtime

Managed memory supports semantic retrieval and summarization while separating users by actorId. Sessions run in isolated Firecracker microVMs and can use managed session storage, Amazon EFS, or Amazon S3 Files.

### Observability, evaluation, and export

Logs and traces feed CloudWatch GenAI Observability. AgentCore Evaluations measures quality, endpoint versions support staging, production, and rollback, and advanced users can export a harness into Strands code.

## 3. Strands defaults and Lifecycle Hooks

Recent capabilities include:

- Prompt caching, conversation summarization, and context offloading to reduce token usage.
- Built-in tools such as todo_write, subagent, and web_fetch, with separate read, write, and edit permissions.
- Four lifecycle hooks: before_invocation, before_tool_call, after_tool_call, and after_invocation.

Lifecycle hooks add deterministic policy checks. A Lambda function attached to before_tool_call can reject refunds above a threshold, with failureMode defaulting to deny when the check fails or times out. Hooks can also publish asynchronous events to Amazon SNS or Amazon EventBridge.

## 4. Cost and permission controls

- Harness itself has no separate charge; users pay for underlying components and consumed resources.
- AgentCore Runtime charges for active CPU and memory consumption, with pricing varying by Region.
- Leaving allowedTools empty or setting a wildcard can make future built-in tools available automatically. Applications with fixed boundaries should list explicit tools and protect high-risk actions with before_tool_call hooks.

## Takeaway

The difference between an agent demo and a production agent lies in the harness. Amazon Bedrock AgentCore Harness combines isolated runtime, managed memory, tools, observability, evaluation, and lifecycle hooks so teams can control reliability, security, and cost without rebuilding the entire orchestration layer.

## References

- [Amazon Bedrock AgentCore harness is now generally available — AWS AI Blog](https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-agentcore-harness-is-now-generally-available-go-from-idea-to-production-grade-agent-in-minutes/)
- [AgentCore harness adds Strands defaults, built-in tools, and lifecycle hooks — AWS AI Blog](https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-agentcore-harness-adds-strands-harness-defaults-built-in-tools-and-lifecycle-hooks/)
- [Image source — AWS AI Blog](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2026/06/11/ML-20804-1.png)
