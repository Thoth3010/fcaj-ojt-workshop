---
title: "Week 5 Worklog"
date: 2026-11-23
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

{{% notice info %}}
📝 **`[TODO - Update later]`:** Review and adjust daily work items below to match your exact personal schedule if needed.
{{% /notice %}}

### Week 5 Objectives (12/10/2026 – 16/10/2026)

* Master AWS observability and secret management: **Amazon CloudWatch**, **Amazon SNS**, and **SSM Parameter Store**.
* Analyze requirements for the **SEAL / FCAJ Hackathon System** and onboard as **AI Engineer**.

### Daily Worklog

| Day | Tasks | Start Date | Completion Date | References |
| :-: | :--- | :---: | :---: | :--- |
| **Mon** | - Studied **Amazon CloudWatch**: Log Groups, Log Insights queries, metrics, and threshold alarms. | 12/10/2026 | 12/10/2026 | <https://docs.aws.amazon.com/cloudwatch/> |
| **Tue** | - Created an **Amazon SNS** topic, confirmed email subscription, and wired a CloudWatch Alarm for DLQ depth (`> 0`). | 13/10/2026 | 13/10/2026 | <https://docs.aws.amazon.com/sns/> |
| **Wed** | - Stored encrypted `SecureString` secrets in **SSM Parameter Store** and verified scoped IAM read access. | 14/10/2026 | 14/10/2026 | <https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html> |
| **Thu** | - Team kick-off for **SEAL Hackathon System**; reviewed SRS, business rules, and judge scoring workflows. | 15/10/2026 | 15/10/2026 | `docs/documents/ProjectRequirements.md` |
| **Fri** | - Scoped the **AI Judge Assistant**: rubric-aligned code grading with verifiable file/line-number evidence. | 16/10/2026 | 16/10/2026 | <https://docs.aws.amazon.com/wellarchitected/> |

### Week 5 Key Achievements

* Built end-to-end automated alerting from CloudWatch Alarms to email via Amazon SNS.
* Adopted SSM Parameter Store `SecureString` so sensitive keys never touch Git repositories.
* Defined the functional and non-functional scope for the `ai-worker/` subsystem.
