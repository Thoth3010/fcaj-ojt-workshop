---
title: "Blog 1 - Cost Optimization for Local LLM on AWS EC2"
date: 2026-11-23
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

{{% notice info %}}
🔗 **AWS Study Group Post Link:** [Facebook post](https://www.facebook.com/share/p/1FJJYqU4Rp/)
{{% /notice %}}

# Cost Optimization Strategies for Deploying Local LLMs (Qwen3) on AWS EC2 GPU with Amazon SQS

While building the AI Judge assistant for the **SEAL Hackathon Platform**, we faced a classic cloud engineering challenge: *How do you run capable open-weight models (`Qwen3-14B` / `Qwen3-30B-A3B`) privately inside an AWS VPC while staying under a `$20/month` (`~500,000 VND`) student PoC budget?*

---

## 1. The Always-On GPU Trap

In `ap-southeast-1` (Singapore), an On-Demand `g4dn.xlarge` (NVIDIA T4 16GB VRAM) costs roughly **`$0.526/hour`** (`~$383/month` 24/7), while `g5.xlarge` (24GB VRAM) costs **`$1.006/hour`**. Yet hackathon grading happens in concentrated bursts—leaving the GPU idle over 90% of the month.

---

## 2. Three Practical Cost Optimization Levers

### Lever 1: Decoupling with Amazon SQS for On-Demand Compute Windows
Instead of synchronous HTTP calls from Backend to the AI server:
1. The Spring Boot API pushes a job envelope (`fcaj.ai.message.v1`) into **Amazon SQS (`fcaj-ai-jobs-queue`)** and returns `202 Accepted` immediately.
2. Between grading windows, the **EC2 GPU Worker stays `Stopped` (`$0/hr` compute)** while SQS safely retains queued jobs (up to 14 days).
3. During demo or judging sessions, the EC2 worker boots (paired with a fail-safe `shutdown -h +45`), drains the queue on **EC2 Spot pricing (`~$0.16–$0.20/hr`, ~70% discount)**, and shuts down—costing only **`$3.20 – $4.00`** for 20 active hours/month.

### Lever 2: KV-Cache Quantization (`q8_0`) & Flash Attention
To fit 16k-token repository contexts inside a `16GB VRAM` T4 (`g4dn.xlarge`) rather than paying 2x for a `24GB` `g5.xlarge`, we configured Ollama with:
```ini
Environment="OLLAMA_FLASH_ATTENTION=1"
Environment="OLLAMA_KV_CACHE_TYPE=q8_0"
Environment="OLLAMA_KEEP_ALIVE=-1"
```
This cuts context **KV-Cache VRAM consumption by ~50%** without degrading code-review quality.

### Lever 3: Fast Non-Thinking Mode (`/no_think`) + Smart Repo Slicing
Reasoning models like `Qwen3` emit long `<think>...</think>` chains by default, inflating inference latency by 2–3x. Combining the `/no_think` directive with `code_cleaner.py` (filtering lockfiles/binaries while preserving original source line numbers) cut per-job execution time by **~65%**, tripling throughput per billed GPU hour.

---

## 3. Takeaway
Combining **event-driven buffering (Amazon SQS)** with **inference-level tuning (`q8_0`, `/no_think`, `Smart Repo Slicing`)** slashes monthly GPU bills from **`$383/mo`** down to **`~$3.20 – $6.00/mo`**.
