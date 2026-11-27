---
title: "Week 7 Worklog"
date: 2026-11-23
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives (26/10/2026 – 31/10/2026)

* Complete **Module 06 (Databases on AWS)**: `06-01` to `06-03` (RDS, Aurora, Redshift, ElastiCache), `Lab 05` (VPC + EC2 + RDS & Backup/Restore), and `Lab 43` (AWS DMS & Schema Conversion).
* **SEAL Hackathon Project:** Implement `schema.py`, `code_cleaner.py`, and align `mock_worker.py` / `sample_output.json` with BE1.
* Attend **AWS First Cloud AI Journey Community Day 2026** (31/10/2026).

### Daily Worklog

| Day | Tasks | Start Date | Completion Date | References (FCAJ Course & Project) |
| :-: | :--- | :---: | :---: | :--- |
| **Mon** | - Studied **Module 06 (06-01 → 06-03):** Database concepts, Amazon RDS & Aurora, Redshift & ElastiCache.<br>- Implemented `src/schema.py`. | 26/10/2026 | 26/10/2026 | - [06-01 Database Concepts](https://www.youtube.com/watch?v=OOD2RwWuLRw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [06-02 RDS & Aurora](https://www.youtube.com/watch?v=qbrobQZrokY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [06-03 Redshift & ElastiCache](https://www.youtube.com/watch?v=UvdiRW34aNI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **Tue** | - **Lab 06-Lab05 (2.1 → 7):** VPC, EC2/RDS SGs, DB Subnet Group, RDS instance, Backup & Restore & Cleanup.<br>- Implemented `src/code_cleaner.py`. | 27/10/2026 | 27/10/2026 | - [06-Lab05-2.4 DB Subnet Group](https://www.youtube.com/watch?v=OWjX0FsbX9E&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [06-Lab05-4 Create RDS](https://www.youtube.com/watch?v=SlP-KdSs3IM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [06-Lab05-6 Backup & Restore](https://www.youtube.com/watch?v=7So4xNZJ6bk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **Wed** | - **Lab 06-Lab43 (01 → 10):** Fleet Manager, MSSQL/Oracle source config, Schema Conversion to Aurora MySQL.<br>- Added `_file_priority_key` in `code_cleaner.py`. | 28/10/2026 | 28/10/2026 | - [06-Lab43-02 Fleet Manager](https://www.youtube.com/watch?v=nzvE2DYso38&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [06-Lab43-09 Schema Conv](https://www.youtube.com/watch?v=s-6mXTFXwG8&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- `ai-worker/src/code_cleaner.py` |
| **Thu** | - **Lab 06-Lab43 (11 → 17):** Migration Task/Endpoint, Serverless Migration, Event Notifications, Logs & Memory/Table error troubleshooting.<br>- Aligned `sample_output.json` & `mock_worker.py`. | 29/10/2026 | 29/10/2026 | - [06-Lab43-11 Migration Task](https://www.youtube.com/watch?v=4LoLN6D1UU8&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [06-Lab43-13 Serverless Migration](https://www.youtube.com/watch?v=tWGwAz_Ewk4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)<br>- [06-Lab43-16 Troubleshoot Mem](https://www.youtube.com/watch?v=hB6vXJunUAY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **Fri** | - Verified Local Mock Job handoff with Backend BE1 (exact `line_start`/`line_end` & `criteria_id: 4` evidence). | 30/10/2026 | 30/10/2026 | - `docs/report/local-mock-job-completion-2026-10-27.md`<br>- [06-Lab05-7 Clean Up](https://www.youtube.com/watch?v=0WiTedZTcpQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **Sat** | - **Attended Event 3 — AWS First Cloud AI Journey Community Day 2026 (09:00 – 12:00):** Attended sessions on *Building Software Factories*, *Education*, *AWS Lambda Web Functions*, *Amazon SQS: Building Asynchronous Systems*, *My 3-Month AWS Internship Journey*, and *Open Source Contributing*. | 31/10/2026 | 31/10/2026 | - [Event 3: AWS First Cloud AI Journey Community Day 2026](../../4-eventparticipated/4.3-event3/) |

### Week 7 Key Achievements

* Completed **Module 06 (Databases)**: mastered private RDS deployment (`Lab 05`) and AWS DMS migrations (`Lab 43`).
* Shipped deterministic repository ingestion (`code_cleaner.py`) and passed BE1 mock contract handoff.
* Attended **AWS First Cloud AI Journey Community Day 2026**, gaining practical insights into **AWS Lambda Web Functions**, **Amazon SQS**, and **Open Source** consistency.
