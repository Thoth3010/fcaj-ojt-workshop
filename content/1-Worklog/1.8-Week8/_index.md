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

* Complete `ai_grader.py` with Cloud AI (`DeepSeek` / `Gemini`), weighted-score post-processing, and `redact_secrets`.
* Benchmark on the real sample repo (`lead-hackathon-test`) and expand automated Unit & Integration Tests.

### Daily Worklog

| Day | Tasks | Start Date | Completion Date | References |
| :-: | :--- | :---: | :---: | :--- |
| **Mon** | - Engineered `SYSTEM_PROMPT` enforcing evidence bounds (1–3 citations/criterion), anti-hallucination, and `THIEU_DU_LIEU` rules. | 02/11/2026 | 02/11/2026 | `ai-worker/src/ai_grader.py` |
| **Tue** | - Added security guards: `<CANDIDATE_SOURCE_CODE>` prompt-injection isolation, `strip_line_number_prefix()`, and `redact_secrets()`. | 03/11/2026 | 03/11/2026 | `ai-worker/src/ai_grader.py` |
| **Wed** | - Implemented deterministic Python `compute_weighted_overall_score()` and `finish_reason` truncation checks. | 04/11/2026 | 04/11/2026 | `ai-worker/src/schema.py` |
| **Thu** | - Executed live grading benchmark on `lead-hackathon-test` (49 files, 7,257 LOC) via DeepSeek API (`19.71s`, `~$0.0175/job`). | 05/11/2026 | 05/11/2026 | `ai-worker/docs/ai_worker_review_and_decision_report.md` |
| **Fri** | - Authored and verified automated test suite (`tests/test_ai_worker.py` — `10/10` -> `13/13 PASS`). | 06/11/2026 | 06/11/2026 | `ai-worker/tests/test_ai_worker.py` |

### Week 8 Key Achievements

* Shipped hardened `ai_grader.py` with automatic secret masking (`***REDACTED***`) and prompt-injection defense.
* Eliminated LLM arithmetic mistakes via deterministic Python post-processing.
* Reached 100% passing test suite coverage with real token cost metrics (`~$0.0175/job`).
