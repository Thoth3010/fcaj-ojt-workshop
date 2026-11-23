---
title: "Week 8 Worklog"
date: 2026-11-23
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

{{% notice info %}}
📝 **`[TODO - Update later]`:** Review and adjust daily work items below to match your exact personal schedule if needed.
{{% /notice %}}

### Week 8 Objectives (02/11/2026 – 06/11/2026)

* Complete **Module 07 (Part 1 — DynamoDB Serverless Event-Driven, Cost Tagging & AWS SDK)**: `Lab 39`, `Lab 40`, `Lab 60`.
* **SEAL Hackathon Project:** Implement `ai_grader.py`, `redact_secrets()`, run Cloud AI benchmark (`19.71s`), and build automated unit tests.

### Daily Worklog

| Day | Tasks | Start Date | Completion Date | References (FCAJ Course & Project) |
| :-: | :--- | :---: | :---: | :--- |
| **Mon** | - **Lab 07-Lab39 (1 → 5):** Hands-on DynamoDB Console, Backup, and Clean up.<br>- Engineered `SYSTEM_PROMPT` citation bounds in `ai_grader.py`. | 02/11/2026 | 02/11/2026 | - [07-Lab39-1 DynamoDB HOL](https://www.youtube.com/watch?v=w5bqLYPv6DA&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab39-4 Backup](https://www.youtube.com/watch?v=2nXUaTT1uoE&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/src/ai_grader.py` |
| **Tue** | - **Lab 07-Lab39 (6 → 8):** DynamoDB Advanced Patterns, Global Serverless App & **Serverless Event-Driven Architecture (LEDA)**.<br>- Added `<CANDIDATE_SOURCE_CODE>` prompt-injection guard & `redact_secrets()`. | 03/11/2026 | 03/11/2026 | - [07-Lab39-6 Advanced Patterns](https://www.youtube.com/watch?v=kTroCGJwA3g&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab39-7 Global Serverless](https://www.youtube.com/watch?v=eP_cB6SZQ1Q&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab39-8 Serverless LEDA](https://www.youtube.com/watch?v=F3fvIgeetGw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **Wed** | - **Lab 07-Lab40 (2.1 → 4):** Database **Cost, Tagging & Cost Allocation**, Usage tracking & Clean up.<br>- Added `compute_weighted_overall_score()` & `max_tokens` truncation guard. | 04/11/2026 | 04/11/2026 | - [07-Lab40-3.2 Cost](https://www.youtube.com/watch?v=vj53iTVV794&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab40-3.3 Tagging & Cost](https://www.youtube.com/watch?v=oFaX_1TggjQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab40-4 Clean Up](https://www.youtube.com/watch?v=ggFZt2JGIeM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **Thu** | - **Lab 07-Lab60 (1 → 3):** AWS operations via **CloudShell, Console & AWS SDK**.<br>- Benchmarked `lead-hackathon-test` (49 files, 7,257 LOC) via DeepSeek API (`19.71s`, `~$0.0175/job`). | 05/11/2026 | 05/11/2026 | - [07-Lab60-1 CloudShell](https://www.youtube.com/watch?v=cqczgtnvHjc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab60-3 AWS SDK](https://www.youtube.com/watch?v=gjY6l4elopw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/docs/ai_worker_review_and_decision_report.md` |
| **Fri** | - Built and verified automated test suite `tests/test_ai_worker.py` (`10/10` -> `13/13 PASS`). | 06/11/2026 | 06/11/2026 | - `ai-worker/tests/test_ai_worker.py` |

### Week 8 Key Achievements

* Mastered **Serverless Event-Driven Architecture (`Lab 39`)**, cost-allocation tagging (`Lab 40`), and AWS SDK usage (`Lab 60`).
* Delivered `ai_grader.py` achieving `19.71s/job` (`~$0.0175/job`), automated secret redaction, and deterministic weighted scoring.
