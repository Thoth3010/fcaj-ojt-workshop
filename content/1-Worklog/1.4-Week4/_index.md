---
title: "Week 4 Worklog"
date: 2026-11-23
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

{{% notice info %}}
📝 **`[TODO - Update later]`:** Review and adjust daily work items below to match your exact personal schedule if needed.
{{% /notice %}}

### Week 4 Objectives (05/10/2026 – 09/10/2026)

* Master **Serverless & Event-Driven** building blocks: **AWS Lambda**, **Amazon SQS**, and **Dead-Letter Queues (DLQs)**.
* Study managed relational databases (**Amazon RDS MySQL**) and edge protection (**AWS WAF / CloudFront**).

### Daily Worklog

| Day | Tasks | Start Date | Completion Date | References |
| :-: | :--- | :---: | :---: | :--- |
| **Mon** | - Studied **Amazon SQS**: Standard vs. FIFO, Long Polling (`20s`), `VisibilityTimeout`, and `RedrivePolicy` to **DLQ**. | 05/10/2026 | 05/10/2026 | <https://docs.aws.amazon.com/sqs/> |
| **Tue** | - Studied **AWS Lambda** (Python 3.12): SQS Event Source Mapping, `ReportBatchItemFailures`, and `MaximumConcurrency`. | 06/10/2026 | 06/10/2026 | <https://docs.aws.amazon.com/lambda/> |
| **Wed** | - Provisioned SQS + DLQ pairs and tested a Python Lambda consumer reading SQS messages via AWS CLI. | 07/10/2026 | 07/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| **Thu** | - Reviewed **Amazon RDS MySQL 8.4**: Private DB Subnet Groups, TLS enforcement, and automated snapshots. | 08/10/2026 | 08/10/2026 | <https://docs.aws.amazon.com/rds/> |
| **Fri** | - Studied **AWS WAF** rate-limiting/managed rule sets and **Amazon ECR** container registry workflows. | 09/10/2026 | 09/10/2026 | <https://docs.aws.amazon.com/waf/> |

### Week 4 Key Achievements

* Learned how SQS + DLQ buffers asynchronous workloads and prevents infinite retry loops on poison messages.
* Tested SQS-to-Lambda event triggers with `BatchSize=1` and partial batch failure reporting.
* Understood secure RDS placement inside private subnets accessible solely from the Backend Security Group.
