---
title: "Blog 2 - Fault-Tolerant Pipeline with SQS, DLQ & S3 Idempotency"
date: 2026-11-23
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

{{% notice info %}}
🔗 **AWS Study Group Post Link:** `[TODO - Update later: Paste the live URL of your post in the AWS Study Group Facebook group or awsstudygroup.com]`
{{% /notice %}}

# Designing a Fault-Tolerant Asynchronous Pipeline with Amazon SQS, Dead-Letter Queues (DLQ), and S3 Idempotency

AI inference jobs typically take 15 to 60 seconds—far too long for synchronous HTTP request-response cycles. In the **SEAL Hackathon Platform**, we built a decoupled asynchronous pipeline on AWS. Here are the key architectural patterns that keep it resilient.

---

## 1. Dual-Queue + Dual-DLQ Topology

Communication between the Backend API and the AI Worker is split into two independent channels:
- **`fcaj-ai-jobs-queue` (+ `fcaj-ai-jobs-dlq`):** Carries `AI_JOB_REQUESTED` envelopes from Backend to Worker.
- **`fcaj-ai-results-queue` (+ `fcaj-ai-results-dlq`):** Carries `AI_JOB_COMPLETED` / `FAILED` notifications back to the Backend.

Setting a **`RedrivePolicy` with `maxReceiveCount = 3`** ensures poison messages are isolated into the DLQ after three failed attempts—preventing infinite retry loops that waste LLM tokens or Lambda invocations.

---

## 2. Handling At-Least-Once Delivery & Visibility Timeouts

**Amazon SQS Standard Queues** guarantee *at-least-once* delivery, and if processing outlasts `VisibilityTimeout`, another consumer will pick up the same message. To achieve safe idempotent processing:

1. **Claim-Check Pattern with Amazon S3:** Keep SQS messages lightweight (`fcaj.ai.message.v1`, `< 32 KB`) containing S3 pointers plus **SHA-256** checksums for `source.json` and `rubric.json`.
2. **Background SQS Heartbeat:** While local inference runs on EC2, a background thread periodically invokes `sqs.change_message_visibility()` so SQS never re-dispatches an active job prematurely.
3. **Conditional Idempotent S3 Writes (`If-None-Match: "*"`):**
   ```python
   s3_client.put_object(
       Bucket=bucket,
       Key=f"{prefix}/results/{job_id}/output.json",
       Body=payload_bytes,
       ContentType="application/json",
       IfNoneMatch="*",
   )
   ```
   Using S3 conditional `IfNoneMatch="*"` guarantees that even if a retry occurs, an existing output artifact is never silently overwritten.

---

## 3. Proactive Failure Detection with CloudWatch & SNS

By attaching a **CloudWatch Alarm** to `ApproximateNumberOfMessagesVisible > 0` on both DLQs and wiring it to **Amazon SNS**, operators receive immediate email alerts whenever a job lands in a DLQ so it can be inspected and redriven cleanly.
