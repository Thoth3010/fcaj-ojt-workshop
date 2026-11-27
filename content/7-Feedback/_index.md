---
title: "Sharing and Feedback"
date: 2026-11-23
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

> Joining the **First Cloud AI Journey (FCAJ)** program has been an important stepping stone in bridging academic study at **FPT University** with practical **AWS** engineering standards. Beyond helping me systematically build foundational Cloud knowledge, the program kept me up to date with emerging trends in **Generative AI**, **RAG**, and **Agentic AI** through its curriculum, community, and live events.

### Overall Evaluation

**1. Overall Satisfaction:** **Very Satisfied (5/5)**.

What I valued most was being able to connect the lessons to the team project. The labs helped me get familiar with individual services. In the SEAL project, I had to think about how those services fit together and how to verify that the processing flow worked. Keeping a weekly worklog helped me see what I had practiced and where I needed more time.

**2. Learning Progression**\
A well-structured learning progression from Cloud fundamentals (`Cloud Foundations`, `VPC`, `EC2`, `S3`, `IAM`) to modern services (`Serverless`, `Event-Driven`, `AI/GenAI`).

The early lessons showed me how networking, permissions, and storage fit into an AWS system. When I reached Lambda and SQS, that foundation helped me understand why SEAL used a queue between receiving submissions and grading them with AI. I also had the chance to deploy a model with Ollama and Qwen3 on EC2 and measure its processing time.

**3. Security and Cost Governance**\
Strong emphasis on security and cost governance from the very first labs (`MFA`, `IAM Least Privilege`, `AWS Budgets`, and resource clean-up).

The labs made checking IAM permissions, setting budget alerts, and cleaning up resources part of my routine. In the AI grading project, the same mindset led to questions about which data the worker should access and how to keep sensitive information out of model inputs. Working on the data preparation step showed me how those decisions shape the processing flow.

**4. Community and Events**\
The **AWS Study Group VN** community and in-person events (`Buildathon Kick-off`, `AWS Cloud & AI Day Hanoi`, `Community Day`) create an open, supportive environment to learn directly from mentors and practitioners.

Writing three technical posts helped me learn in a different way. To explain AWS MCP Server, IaC, and AgentCore Harness to readers who were new to the topics, I had to revisit the documentation and think carefully about how to describe what each tool does. I want to keep improving that skill alongside my confidence in live presentations.

---

### Additional Questions

- **Would I Recommend FCAJ to Friends? Why?**\
  **Definitely YES.**\
  **Why:** FCAJ provides a proactive, industry-aligned learning environment that stays closely connected to fast-moving technologies—especially Cloud + AI. Beyond preparing for AWS certifications, the program builds strong habits in technical writing, community sharing, and architectural thinking, which are invaluable for any IT/AI student entering the industry.

  For someone new to cloud, I would suggest following the lessons in order, repeating the main lab steps, and writing down one thing they learned each time. For someone interested in AI, the team project is a chance to put a model into a workflow that uses storage, a queue, and monitoring.

---

### Suggestions & Expectations

- The volume of labs and lessons becomes fairly dense during the middle weeks; adding concise cheat-sheets of common `IAM` and `VPC` misconfigurations per module would help newcomers troubleshoot faster.
- Extending the duration of short **Hands-on mini challenges** during offline events would give attendees more time for direct, on-the-spot Q&A with mentors.
- I would also like a group lab that runs through an entire workflow, from submitting data and queuing a job to running an AI grader and checking the result and logs. At the end, each group could share one design decision and one issue they ran into, then compare how they handled them.
