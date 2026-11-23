---
title: "Week 9 Worklog"
date: 2026-11-23
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

{{% notice info %}}
📝 **`[TODO - Update later]`:** Review and adjust daily work items below to match your exact personal schedule if needed.
{{% /notice %}}

### Week 9 Objectives (09/11/2026 – 13/11/2026)

* Design and benchmark running **Local AI (`Ollama + Qwen3`) directly on AWS EC2** inside the VPC.
* Provision a live EC2 instance in `ap-southeast-1`, optimize `KV Cache (q8_0)`, measure E2E latency, and tear down to `$0.00`.

### Daily Worklog

| Day | Tasks | Start Date | Completion Date | References |
| :-: | :--- | :---: | :---: | :--- |
| **Mon** | - Authored the **EC2 Local AI Proposal** (`ec2_local_ai_proposal.md`) comparing `Qwen3-14B` (`g4dn.xlarge`) vs. `Qwen3-30B-A3B MoE` (`g5.xlarge`). | 09/11/2026 | 09/11/2026 | `ai-worker/docs/ec2_local_ai_proposal.md` |
| **Tue** | - Created `setup_ec2_ollama.sh` automating 4GB swap, `OLLAMA_FLASH_ATTENTION=1`, `OLLAMA_KV_CACHE_TYPE=q8_0`, and fail-safe `shutdown -h +45`. | 10/11/2026 | 10/11/2026 | `ai-worker/scripts/setup_ec2_ollama.sh` |
| **Wed** | - Upgraded `ai_grader.py` to support `provider="local_ai"` (`/v1/chat/completions`), `/no_think` mode, and `<think>` block stripping. | 11/11/2026 | 11/11/2026 | `ai-worker/src/ai_grader.py` |
| **Thu** | - Provisioned EC2 Ubuntu 24.04 (`t3.small` Free Tier) in `ap-southeast-1`, pulled `qwen3` (`8.97s–11.59s`), and measured E2E JSON output (`50.77s`, 100% pass). | 12/11/2026 | 12/11/2026 | `ai-worker/docs/ec2_local_ai_benchmark_report.md` |
| **Fri** | - Verified `13/13` passing tests (`0.032s`), terminated all EC2/EBS/SG/KeyPair resources (`$0.00`), and published benchmark report. | 13/11/2026 | 13/11/2026 | `ai-worker/docs/ec2_local_ai_benchmark_report.md` |

### Week 9 Key Achievements

* Validated **Local AI (`Ollama + Qwen3`) on AWS EC2** achieving 100% JSON contract compliance and automated secret redaction.
* Reduced context VRAM/RAM consumption by ~50% via `OLLAMA_KV_CACHE_TYPE=q8_0` and Smart Repo Slicing.
* Maintained **`$0.00`** net AWS spend through immediate post-benchmark clean-up.
