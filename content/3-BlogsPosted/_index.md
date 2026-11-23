---
title: "Blogs Posted"
date: 2026-11-23
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

{{% notice info %}}
📝 **`[TODO - Update later]`:** Per FCAJ rules, you need to publish **at least 3 quality blogs** to the [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj). Full technical drafts aligned with your AWS & AI project are ready below — simply publish them to the group and paste the **live post URLs** into Blogs 1, 2, and 3!
{{% /notice %}}

### Published Technical Blogs (AWS Study Group)

1. **[Blog 1 - Cost Optimization Strategies for Deploying Local LLMs (Qwen3) on AWS EC2 GPU with Amazon SQS](3.1-Blog1/)**
   - Analyzes why 24/7 GPU instances cost `$380–$720/month` and demonstrates how decoupling via **Amazon SQS** allows on-demand EC2 start/stop alongside `KV Cache (q8_0)` quantization to cut VRAM usage by 50%.
   - *Post URL Status:* `[TODO - Update later: Add live AWS Study Group post link]`

2. **[Blog 2 - Designing a Fault-Tolerant Asynchronous Pipeline with Amazon SQS, DLQ, and S3 Idempotency](3.2-Blog2/)**
   - Covers message contract design (`fcaj.ai.message.v1`), `VisibilityTimeout` heartbeat extension, `RedrivePolicy` DLQ isolation, and idempotent S3 writes using `If-None-Match: "*"`.
   - *Post URL Status:* `[TODO - Update later: Add live AWS Study Group post link]`

3. **[Blog 3 - Securing AI Workloads on AWS: IAM Least Privilege, SSM Parameter Store & Secret Redaction](3.3-Blog3/)**
   - Practical patterns for scoping AI Worker IAM roles, retrieving secrets from `SSM SecureString`, isolating untrusted code against Prompt Injection, and deterministic secret redaction.
   - *Post URL Status:* `[TODO - Update later: Add live AWS Study Group post link]`
