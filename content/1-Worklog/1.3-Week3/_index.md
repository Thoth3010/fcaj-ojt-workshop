---
title: "Week 3 Worklog"
date: 2026-11-23
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

{{% notice info %}}
📝 **`[TODO - Update later]`:** Review and adjust daily work items below to match your exact personal schedule if needed.
{{% /notice %}}

### Week 3 Objectives (28/09/2026 – 02/10/2026)

* Implement **AWS IAM** policies and roles following strict **Least Privilege** principles.
* Master **Amazon S3**: Bucket Policies, Block Public Access, SSE-S3 encryption, Lifecycle rules, and Gateway Endpoints.

### Daily Worklog

| Day | Tasks | Start Date | Completion Date | References |
| :-: | :--- | :---: | :---: | :--- |
| **Mon** | - Studied **IAM Policy** evaluation logic, Identity vs. Resource policies, IAM Roles, and Trust Policies. | 28/09/2026 | 28/09/2026 | <https://docs.aws.amazon.com/iam/> |
| **Tue** | - Authored fine-grained IAM Policies scoped to exact ARNs and S3 prefixes instead of broad managed policies. | 29/09/2026 | 29/09/2026 | <https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html> |
| **Wed** | - Explored **Amazon S3** storage classes, versioning, Block Public Access, and conditional writes (`If-None-Match: "*"`). | 30/09/2026 | 30/09/2026 | <https://docs.aws.amazon.com/s3/> |
| **Thu** | - Created a private S3 bucket with Block Public Access enabled and Lifecycle expiration rules after 30 days. | 01/10/2026 | 01/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| **Fri** | - Practiced **S3 Gateway Endpoint** routing inside VPC and **CloudFront Origin Access Control (OAC)** for private static sites. | 02/10/2026 | 02/10/2026 | <https://docs.aws.amazon.com/AmazonCloudFront/> |

### Week 3 Key Achievements

* Gained fluency writing prefix-scoped Least Privilege IAM policies for compute and serverless workers.
* Configured private S3 storage with automated Lifecycle rules and CloudFront OAC protection.
* Understood how S3 Gateway Endpoints keep traffic inside AWS while eliminating NAT egress costs.
