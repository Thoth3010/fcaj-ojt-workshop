---
title: "Week 7 Worklog"
date: 2026-11-23
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

{{% notice info %}}
📝 **`[TODO - Update later]`:** Review and adjust daily work items below to match your exact personal schedule if needed.
{{% /notice %}}

### Week 7 Objectives (26/10/2026 – 30/10/2026)

* Build the source ingestion and sanitation module (`code_cleaner.py`) with accurate line-number tagging.
* Synchronize `schema.py`, `mock_worker.py`, and integration fixtures with Backend BE1.

### Daily Worklog

| Day | Tasks | Start Date | Completion Date | References |
| :-: | :--- | :---: | :---: | :--- |
| **Mon** | - Implemented `src/schema.py` data models (`GradingJobInput`, `GradingJobOutput`, `CriterionResult`, `CodeEvidence`). | 26/10/2026 | 26/10/2026 | `ai-worker/src/schema.py` |
| **Tue** | - Implemented `src/code_cleaner.py` to exclude build/dependency dirs (`node_modules`, `target`), binaries, and lockfiles while tagging line numbers. | 27/10/2026 | 27/10/2026 | `ai-worker/src/code_cleaner.py` |
| **Wed** | - Added `_file_priority_key` to prioritize core source directories (`src/`, `app/`, `back-end/`) within `max_total_chars`. | 28/10/2026 | 28/10/2026 | `ai-worker/contracts/` |
| **Thu** | - Aligned `sample_output.json` & `mock_worker.py`: fixed `line_start`/`line_end` accuracy and added missing `criteria_id: 4` evidence. | 29/10/2026 | 29/10/2026 | `ai-worker/src/mock_worker.py` |
| **Fri** | - Verified local mock job handoff with BE1 and documented integration readiness. | 30/10/2026 | 30/10/2026 | `docs/report/local-mock-job-completion-2026-10-27.md` |

### Week 7 Key Achievements

* Delivered deterministic repository collection that preserves exact source line numbers for AI citations.
* Achieved 100% alignment between `mock_worker.py`, `sample_output.json`, and Backend validators.
* Signed off on the Local Mock Job milestone with the Backend team.
