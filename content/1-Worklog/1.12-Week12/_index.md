---
title: "Week 12 Worklog"
date: 2026-11-23
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

{{% notice info %}}
📝 **`[TODO - Update later]`:** Review and adjust daily work items below to match your exact personal schedule (remember the rule to submit the Workshop **15 days prior to needing your internship stamp**).
{{% /notice %}}

### Week 12 Objectives (30/11/2026 – 04/12/2026)

* Record and verify the **Live Demo** of the working E2E system (SQS -> AI Worker -> S3 Results -> CloudWatch Logs).
* Finalize all evidence (3 AWS Study Group blogs, 3 Events with clear check-in photos) and complete full AWS resource clean-up.

### Daily Worklog

| Day | Tasks | Start Date | Completion Date | References |
| :-: | :--- | :---: | :---: | :--- |
| **Mon** | - Rehearsed full E2E pipeline flow from `fcaj-ai-jobs-queue` dispatch to verified JSON output on S3 and `fcaj-ai-results-queue`. | 30/11/2026 | 30/11/2026 | `content/5-Workshop/5.5-Testing-Monitoring/` |
| **Tue** | - Performed fault injection test: dispatched malformed payload to verify DLQ routing and **CloudWatch Alarm -> SNS Email** trigger. | 01/12/2026 | 01/12/2026 | <https://docs.aws.amazon.com/cloudwatch/> |
| **Wed** | - Recorded Live Demo proof, updated AWS Study Group blog URLs, 3 event check-in photos, and personal avatar. | 02/12/2026 | 02/12/2026 | `content/` |
| **Thu** | - Executed complete **Resource Clean-up** (Lambda, SQS/DLQs, empty & delete S3 bucket, SSM, CloudWatch Alarms) and verified `$0.00` bill. | 03/12/2026 | 03/12/2026 | `content/5-Workshop/5.6-Cleanup/` |
| **Fri** | - Completed final bilingual quality audit and submitted Workshop link at least 15 days ahead of the stamp deadline. | 04/12/2026 | 04/12/2026 | <https://hcm-rules.awsfcaj.com/project> |

### Week 12 Key Achievements

* Completed 100% of FCAJ OJT requirements on time.
* Verified functional, security, and observability behavior end-to-end.
* Left the AWS account completely clean with zero lingering billable resources.
