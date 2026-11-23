---
title: "Self-evaluation"
date: 2026-11-23
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

{{% notice info %}}
📝 **`[TODO - Update later]`:** This self-evaluation table has been drafted based on your work on the SEAL Hackathon & AI Judge Worker project. Please review and personalize the ratings (**Good / Fair / Average**) and specific reflections before final submission.
{{% /notice %}}

### Internship Self-Evaluation Matrix (8 Mandatory Criteria)

| No. | Evaluation Criteria | Self-Rating | Specific Reflection & Evidence |
| :-: | :--- | :---: | :--- |
| 1 | **Technical Knowledge** | **Good** | Solid grasp of core AWS services (`EC2`, `VPC`, `IAM`, `S3`, `SQS`, `Lambda`, `RDS`, `SSM`, `CloudWatch`). Applied AI engineering skills to integrate `Qwen3` (Ollama) and Cloud AI APIs (`DeepSeek` / `Gemini`) into an asynchronous code-evaluation pipeline with 100% JSON schema compliance. |
| 2 | **Self-Learning & Research** | **Good** | Independently researched `KV Cache quantization (q8_0)`, Flash Attention, structured JSON output constraints, and the AWS Well-Architected Framework to optimize inference speed and keep cloud spending minimal on Free Tier and Spot instances. |
| 3 | **Proactiveness** | **Good** | Proactively identified VRAM bottlenecks, designed the Smart Repo Slicing mechanism (`code_cleaner.py`), and executed live EC2 benchmarks in `ap-southeast-1` to provide quantitative decision data for the team. |
| 4 | **Discipline & Compliance** | **Good** | Strictly enforced security hygiene (zero hardcoded secrets, automatic secret redaction, `IAM Least Privilege`, `SSM Parameter Store`), performed complete post-lab resource clean-up (`$0.00` unintended charges), and maintained consistent worklogs. |
| 5 | **Communication Skills** | **Fair** | Authored clear bilingual technical proposals, benchmark reports, and integration contracts. Continuing to refine concise verbal storytelling during live technical demos. |
| 6 | **Teamwork** | **Good** | Collaborated closely with the Team Lead, Backend (BE1/BE2), and Frontend teams to standardize the `fcaj.ai.message.v1` / `fcaj.ai.output.v1` contracts and validate end-to-end SQS/S3 integration smoothly. |
| 7 | **Problem-Solving Capability** | **Good** | Resolved 4 key engineering challenges: context overflow on 90k+ token repos (`Smart Repo Slicing`), LLM weighted-score miscalculation (`Python post-processing`), secret leakage in evidence (`redact_secrets`), and job timeout retries (`SQS Heartbeat` & `DLQ`). |
| 8 | **Contribution to Workshop** | **Good** | Designed and implemented an end-to-end personal technical workshop on **Asynchronous AI Code Judge Pipeline on AWS**, complete with provisioning commands, automated unit/integration tests (`13/13 PASS`), cost estimation, and clean-up procedures. |

---

### Post-Internship Growth Goals

- Deepen hands-on expertise in Infrastructure as Code (**Terraform / AWS CDK**) to provision multi-tier VPC, SQS, S3, Lambda, and GPU EC2 stacks declaratively.
- Strengthen live English technical presentation skills and design larger-scale fault-tolerant distributed AI workloads with end-to-end observability.
