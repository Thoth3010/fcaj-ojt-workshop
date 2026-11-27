---
title: "Week 9 Worklog"
date: 2026-11-23
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives (09/11/2026 – 13/11/2026)

* Complete **Module 07 (Part 2 — Data Pipeline, Firehose, Glue, DataBrew, EMR, Athena, Kinesis, QuickSight & Lambda Serving)**: `Lab 35`, `Lab 70`, `Lab 72`, `Lab 73`.
* **SEAL Hackathon Project:** Migrate & run live **Local AI (`Ollama + Qwen3`) benchmarks on AWS EC2 (`ap-southeast-1`)**, tune `q8_0` KV-cache, and clean up to `$0.00`.

### Daily Worklog

| Day | Tasks | Start Date | Completion Date | References (FCAJ Course & Project) |
| :-: | :--- | :---: | :---: | :--- |
| **Mon** | - **Lab 07-Lab35 (3.1 → 7):** S3, Firehose Delivery Stream, Glue Crawler, Athena, QuickSight & Clean up.<br>- Authored `ec2_local_ai_proposal.md`. | 09/11/2026 | 09/11/2026 | - [07-Lab35-3.2 Delivery Stream](https://www.youtube.com/watch?v=a85LUgxpPUI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab35-4.1 Glue Crawler](https://www.youtube.com/watch?v=MQRJ_v8HYHM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/docs/ec2_local_ai_proposal.md` |
| **Tue** | - **Lab 07-Lab70 (1.1 → 2.3):** Cloud9 setup, dataset ingestion to S3, Data Profiling & Glue DataBrew transforms.<br>- Wrote `setup_ec2_ollama.sh` (4GB swap, `OLLAMA_FLASH_ATTENTION=1`, `OLLAMA_KV_CACHE_TYPE=q8_0`, `shutdown -h +45`). | 10/11/2026 | 10/11/2026 | - [07-Lab70-2.1 DataBrew](https://www.youtube.com/watch?v=T-OPhEXdo9Y&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab70-2.3 Clean Data](https://www.youtube.com/watch?v=O-xRfw94xlY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/scripts/setup_ec2_ollama.sh` |
| **Wed** | - **Lab 07-Lab72 (2 → 8):** Ingest, Catalog, AWS Glue (Interactive/GUI), DataBrew & EMR transforms.<br>- Upgraded `ai_grader.py` with default `local_ai` provider (`/no_think` + `<think>` stripping). | 11/11/2026 | 11/11/2026 | - [07-Lab72-5 Glue Interactive](https://www.youtube.com/watch?v=Eym-acAcD6s&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab72-8 Transform EMR](https://www.youtube.com/watch?v=PSBYrhMW-8g&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/src/ai_grader.py` |
| **Thu** | - **Lab 07-Lab72 (9 → 13) & Lab73 (3 → 5):** Athena, Kinesis Analytics, QuickSight, **Serve with Lambda**, Redshift & Dashboards.<br>- Launched EC2 Ubuntu 24.04 (`t3.small` Free Tier in `ap-southeast-1`), pulled Qwen3 (`8.97s–11.59s`), measured E2E JSON (`50.77s`, 100% pass). | 12/11/2026 | 12/11/2026 | - [07-Lab72-12 Serve with Lambda](https://www.youtube.com/watch?v=TZUA_0gSlNA&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [07-Lab73-5 Interactive Dashboard](https://www.youtube.com/watch?v=KrTFP_qa0Ww&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/docs/ec2_local_ai_benchmark_report.md` |
| **Fri** | - Passed `13/13` tests (`0.032s`), terminated all EC2/EBS/SG/KeyPair resources (`$0.00`), and submitted the benchmark report. | 13/11/2026 | 13/11/2026 | - `ai-worker/docs/ec2_local_ai_benchmark_report.md`<br>- [07-Lab35-7 Clean Up](https://www.youtube.com/watch?v=r9NehOtENWQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |

### Week 9 Key Achievements

* Completed **Module 07 (Data & Analytics Pipeline + Lambda Serving)** — finishing the core First Cloud Journey video curriculum.
* Proved **Local AI (`Ollama + Qwen3`) on AWS EC2 `ap-southeast-1`** with 100% JSON contract compliance and `$0.00` net spend after cleanup.
