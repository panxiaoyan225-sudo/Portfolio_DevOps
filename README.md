# Portfolio Monitor & Auto-Warmer

Technical implementations of automated infrastructure workflows designed for high-reliability cloud environments. This framework bridges the gap between **Data Engineering efficiency** and **Strategic Risk management** through automated health checks and real-time anomaly detection.

## 🎯 Project Philosophy

Most modern cloud-native applications suffer from "Cold Start" latency on serverless platforms. This project demonstrates a **high-performance, low-footprint architecture** optimized for Google Cloud Run. By transitioning from Microsoft-hosted agents to a **Self-Hosted Windows Agent**, I bypassed environment concurrency limits while maintaining a production-grade CI/CD lifecycle.

## 🏗️ System Architecture

The framework orchestrates infrastructure health through five specialized layers:

1.  **Ingestion Layer:** Hybrid trigger support for both `git push` events and periodic "Heartbeat" triggers via YAML-based `cron` schedules.
2.  **Validation Layer (The Gatekeeper):** A "Fail-Fast" pre-check stage that validates environment variables (e.g., `SLACK_TOKEN`) and performs syntax compilation before script execution.
3.  **Environment Sync:** Automated dependency management and Python 3.11 configuration with native UTF-8 support for cross-platform log compatibility.
4.  **Persistence Layer:** Secure management of sensitive API tokens and URLs using Azure DevOps Variable Groups (`Portfolio-Secrets`).
5.  **Audit & Alerting:** A Slack-integrated monitoring system that detects performance anomalies and pushes real-time status notifications.

## 🔄 The Pipelines

* **Fail-Fast Validation:** Every run begins with a logic gate that ensures credentials are live and the Python code is syntactically sound, preventing "silent failures" in production.
* **Self-Hosted Execution:** Powered by a local Windows agent (**PANPAN**) to ensure zero-cost execution without cloud parallelism restrictions.
* **Cloud Run Warmer:** Periodically pings the hosted portfolio to ensure the container remains warm and responsive, eliminating "Cold Start" latency.
* **Dual-Trigger Logic:** Configured for both continuous integration on every code push and a monthly scheduled maintenance run.

## 🛠️ Technical Stack

* **Cloud Provider:** Google Cloud Platform (Cloud Run)
* **Orchestration:** Azure DevOps (Azure Pipelines)
* **Agent Infrastructure:** Self-Hosted Windows Agent (PowerShell/CMD)
* **Automation:** Python 3.11 & YAML-based CI/CD
* **Monitoring:** Slack API (Webhooks), Requests, aiosmtplib

---

## 🚀 Installation & Setup

### Azure DevOps Configuration
1.  **Agent Setup:** Download and configure a self-hosted agent in the `MyLocalLaptop` pool using a Personal Access Token (PAT).
2.  **Variable Group:** Create a group named `Portfolio-Secrets` and map your `SLACK_TOKEN`.
3.  **Validation Gate:** The pipeline automatically runs an assertion check on your environment variables before the main monitoring script starts.
4.  **Execution:** The `azure-pipelines.yml` handles Windows-specific dependency installation and UTF-8 environment setup.

### Local Development & Testing
```bash
# Create and activate virtual environment
python -m venv venv
venv\Scripts\activate  # On Windows

# Install dependencies
pip install -r requirements.txt

# Run Validation & Monitor Manually
set PYTHONUTF8=1
python -m py_compile monitor_portfolio.py
python monitor_portfolio.py