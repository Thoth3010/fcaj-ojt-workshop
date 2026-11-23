---
title: "Week 10 Worklog"
date: 2026-11-23
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

{{% notice info %}}
📝 **`[TODO - Update later]`:** Review and adjust daily work items below to match your exact personal schedule if needed.
{{% /notice %}}

### Week 10 Objectives (16/11/2026 – 20/11/2026)

* Apply **Serverless Event-Driven (`07-Lab39`, `05-Lab22`)** and **IAM Role (`05-Lab48`)** patterns to the **SEAL Hackathon AWS v3 Architecture**.
* Implement **`src/lambda_handler.py`** and **`src/sqs_worker.py`** matching `fcaj.ai.message.v1` / `fcaj.ai.output.v1`.

### Daily Worklog

| Day | Tasks | Start Date | Completion Date | References (FCAJ Course & Project) |
| :-: | :--- | :---: | :---: | :--- |
| **Mon** | - Studied **SEAL AWS v3** target architecture (`2aOboRCqu5DgDHelB6fUFKkeiAnJaYh3wF1DxO08.md`), revisiting *Serve with Lambda* (`07-Lab72-12`) to keep the AI Worker outside the VPC. | 16/11/2026 | 16/11/2026 | - `ai-worker/README.md`<br>- [07-Lab72-12 Serve with Lambda](https://www.youtube.com/watch?v=TZUA_0gSlNA&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **Tue** | - Built `src/lambda_handler.py`: strict **SHA-256** & `sizeBytes` verification for `input-manifest.json`, `source.json`, and `rubric.json` on S3. | 17/11/2026 | 17/11/2026 | - `ai-worker/src/lambda_handler.py`<br>- [05-Lab48-3.2 Using IAM Role](https://www.youtube.com/watch?v=Z0liKVSjt_Q&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **Wed** | - Integrated warm-start **SSM Parameter Store** key caching, `safeText` filtering, and idempotent S3 writes (`If-None-Match: "*"`). | 18/11/2026 | 18/11/2026 | - `ai-worker/src/lambda_handler.py`<br>- [07-Lab39-8 Serverless LEDA](https://www.youtube.com/watch?v=F3fvIgeetGw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **Thu** | - Implemented `src/sqs_worker.py` with Long Polling (`WaitTimeSeconds=20`), `VisibilityTimeout=120s`, and temporary `aws login` credentials. | 19/11/2026 | 19/11/2026 | - `ai-worker/src/sqs_worker.py`<br>- [05-Lab22-4 Lambda Role](https://www.youtube.com/watch?v=7_1A2Jxl7_c&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| **Fri** | - Authored and passed v3 contract test suites (`tests/test_lambda_handler_v1.py`, `tests/test_sqs_worker.py`). | 20/11/2026 | 20/11/2026 | - `ai-worker/tests/test_lambda_handler_v1.py`<br>- `ai-worker/tests/test_sqs_worker.py` |

### Week 10 Key Achievements

* Shipped dual production worker modes: **AWS Lambda Serverless** and **EC2/Standalone SQS Poller**.
* Enforced SHA-256 integrity checks and conditional idempotent S3 writes (`If-None-Match: "*"`).
* Passed all automated v3 contract integration tests.
