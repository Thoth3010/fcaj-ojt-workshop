---
title: "Week 6 Worklog"
date: 2026-11-23
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives (19/10/2026 – 23/10/2026)

* Complete **Module 05 (Part 2 — Advanced IAM, Tagging, KMS, CloudTrail & Athena)**: `Lab 27`, `Lab 28`, `Lab 30`, `Lab 33`, `Lab 44`, `Lab 48`.
* **SEAL Hackathon Project:** Finalize `aws-workshop-architecture-plan.md`, JSON Contracts (`input_schema.json`, `output_schema.json`, `fcaj.ai.message.v1`), and AWS Pricing Calculator estimate.

### Daily Worklog

| Day | Tasks | Start Date | Completion Date | References (FCAJ Course & Project) |
| :-: | :--- | :---: | :---: | :--- |
| **Mon** | - **Lab 05-Lab27 & 05-Lab28:** Resource tagging via CLI, Resource Groups, IAM Policies/Roles & Switch Roles.<br>- Team review finalizing **AWS Workshop Architecture Plan**. | 19/10/2026 | 19/10/2026 | - [05-Lab27-2.2 Tags CLI](https://www.youtube.com/watch?v=kYyceAFqsUg&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [05-Lab28-4 IAM Role](https://www.youtube.com/watch?v=pJWANviu8QM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `docs/aws-workshop-architecture-plan.md` |
| **Tue** | - **Lab 05-Lab30 & 05-Lab44:** Built IAM restriction policies and Switch Role conditions by **IP & Time**.<br>- Authored `input_schema.json` and `output_schema.json`. | 20/10/2026 | 20/10/2026 | - [05-Lab30-3 Restriction Policy](https://www.youtube.com/watch?v=MDDYZKU4i6Y&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [05-Lab44-4.3 Limit IP/Time](https://www.youtube.com/watch?v=asMebNbyISQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/contracts/` |
| **Wed** | - **Lab 05-Lab33:** Created KMS keys, S3 encryption, CloudTrail logging & **Amazon Athena** log queries.<br>- Aligned `fcaj.ai.message.v1` contract with BE1/BE2. | 21/10/2026 | 21/10/2026 | - [05-Lab33-3 KMS](https://www.youtube.com/watch?v=XdUKBuwEEr8&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [05-Lab33-5.4 Athena](https://www.youtube.com/watch?v=SWJDiY1fMjQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `docs/contracts/ai-job-v1/` |
| **Thu** | - **Lab 05-Lab48:** Compared long-term Access Keys vs. **EC2 IAM Roles** for S3 access.<br>- Estimated monthly PoC spend using AWS Pricing Calculator. | 22/10/2026 | 22/10/2026 | - [05-Lab48-3.2 Using IAM Role](https://www.youtube.com/watch?v=Z0liKVSjt_Q&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [05-Lab48-4 Clean Up](https://www.youtube.com/watch?v=wl4wIo7UR9Y&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- <https://calculator.aws/> |
| **Fri** | - Scaffolded `ai-worker/` (`src/`, `contracts/`, `tests/`, `docs/`) and completed the architecture proposal. | 23/10/2026 | 23/10/2026 | - `ai-worker/README.md`<br>- [05-Lab33-7 Clean Up](https://www.youtube.com/watch?v=_EydymVG6UI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |

### Week 6 Key Achievements

* Completed **Module 05 (IAM & Security Deep Dive)**: eliminated static Access Keys in favor of **IAM Roles** (`Lab 48`) and KMS/CloudTrail auditing (`Lab 33`).
* Locked in the 6-layer **SEAL Hackathon** architecture and validated JSON integration contracts.
