# 🚦 Watchdog: Asynchronous AI Telemetry & Anomaly Detection

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Redis](https://img.shields.io/badge/redis-%23DD0031.svg?style=for-the-badge&logo=redis&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![FastAPI](https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=Ollama&logoColor=white)

## 📌 Executive Summary
**Watchdog** is a real-time, event-driven AI streaming pipeline designed to process high-frequency telemetry data. Custom-engineered as a digital Engine Control Unit (ECU) monitor for a **Royal Enfield Interceptor Bear 650**, this system analyzes live sensor streams (RPM, oil temperature, speed) at sub-second latency. 

Instead of traditional batch processing or blocking API calls, Watchdog utilizes an asynchronous Redis message broker and non-blocking local LLM inference to detect critical mechanical anomalies in real-time without dropping a single data packet.

## 🏗️ Event-Driven Architecture

```text
┌─────────────────┐      ┌─────────────────┐      ┌─────────────────┐
│  Bear 650 ECU   │      │  Redis Stream   │      │ Async Consumer  │
│  (Producer.py)  │─────▶│  (Message Queue)│─────▶│  (Watchdog)     │
└─────────────────┘      └─────────────────┘      └─────────────────┘
                                                           │
                                                           ▼ (Async HTTPX)
                                                  ┌─────────────────┐
                                                  │ Local Qwen LLM  │
                                                  │ (AI Diagnostic) │
                                                  └─────────────────┘

🚀 Core Engineering Features
High-Throughput Pub/Sub: Built on Redis Streams, capable of queuing and handling massive volumes of concurrent telemetry data without memory bottlenecks.

Non-Blocking AI Inference: Utilizes asyncio and httpx to trigger localized LLM (qwen2.5:7b) diagnostic analysis for detected anomalies while the primary data stream continues uninterrupted.

Weighted Anomaly Injection: The producer simulation uses weighted statistical probability to mirror real-world riding conditions (95% stable cruising, 5% critical spikes).

Two-Tier Diagnostic Engine: * Tier 1 (Algorithmic): Instantaneous bounds-checking (e.g., Redline RPM > 5500, Oil Temp > 115°C).

Tier 2 (Heuristic): Real-time stream generation of AI mechanical diagnostics for contextual failure analysis.

Rich Terminal UI: A highly legible, color-coded hacker dashboard for live server health monitoring using the rich library.

🛠️ Technology Stack
Message Broker: Redis (Dockerized redis:alpine)

Concurrency: Python asyncio, httpx

Local Intelligence: Ollama (qwen2.5:7b)

Terminal Interface: rich

🐳 Quick Start Guide
1. Spin up the Event Broker:

Bash
# Starts the Redis Message Broker in a lightweight container
docker-compose up -d
2. Initialize the AI Watchdog (Consumer):

Bash
# Install asynchronous dependencies
pip install -r requirements.txt

# Start the non-blocking monitoring daemon
python consumer.py
3. Ignite the Telemetry Stream (Producer):
Open a separate terminal window to start blasting data into the queue:

Bash
# Simulates live engine telemetry from the Bear 650
python producer.py
🛡️ Systems Reliability & Scalability
This pipeline demonstrates proficiency in Concurrency and Fault Tolerance. By decoupling the data ingestion from the AI inference using a Redis buffer, the architecture guarantees zero data loss even during hardware CPU spikes or delayed LLM token generation. It is ready to scale from a single 650cc twin-cylinder engine to a massive enterprise IoT fleet.
