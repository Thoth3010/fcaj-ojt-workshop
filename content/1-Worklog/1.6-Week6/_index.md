---
title: "Week 6 Worklog"
date: 2026-11-23
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

{{% notice info %}}
📝 **`[TODO - Update later]`:** Review and adjust daily work items below to match your exact personal schedule if needed.
{{% /notice %}}

### Week 6 Objectives (19/10/2026 – 23/10/2026)

* Finalize the AWS system architecture plan (`docs/aws-workshop-architecture-plan.md`) with the team.
* Design strict JSON data contracts (`contracts/`) decoupling the Spring Boot Backend from the Python AI Worker.

### Daily Worklog

| Day | Tasks | Start Date | Completion Date | References |
| :-: | :--- | :---: | :---: | :--- |
| **Mon** | - Reviewed the **AWS Architecture Plan**: CloudFront/S3 frontend, EC2 Docker backend, private RDS MySQL, and SQS-decoupled AI worker. | 19/10/2026 | 19/10/2026 | `docs/aws-workshop-architecture-plan.md` |
| **Tue** | - Designed `ai-worker/contracts/input_schema.json` and `output_schema.json` (rubrics, commit SHA, criteria_results, line-level evidence). | 20/10/2026 | 20/10/2026 | `ai-worker/contracts/` |
| **Wed** | - Aligned with Backend engineers (BE1/BE2) on the `fcaj.ai.message.v1` envelope (`AI_JOB_REQUESTED`, `AI_JOB_COMPLETED`). | 21/10/2026 | 21/10/2026 | `docs/contracts/ai-job-v1/` |
| **Thu** | - Modeled monthly PoC cloud spend in **AWS Pricing Calculator** targeting `< 500,000 VND/month`. | 22/10/2026 | 22/10/2026 | <https://calculator.aws/> |
| **Fri** | - Finalized the architecture proposal and scaffolded the `ai-worker/` codebase (`src/`, `contracts/`, `tests/`). | 23/10/2026 | 23/10/2026 | `ai-worker/README.md` |

### Week 6 Key Achievements

* Locked in the 6-layer AWS architecture with AI positioned strictly as an advisory assistant.
* Published validated `sample_input.json` and `sample_output.json` contracts for parallel Backend/AI development.
* Verified PoC cost feasibility via AWS Pricing Calculator.
