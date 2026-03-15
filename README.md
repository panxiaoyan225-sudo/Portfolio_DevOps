# Portfolio Monitor & Auto-Warmer

Technical implementations of automated infrastructure workflows designed for high-reliability cloud environments. This framework bridges the gap between **Data Engineering efficiency** and **Strategic Risk management** through automated health checks and real-time anomaly detection.

## 🎯 Project Philosophy

Most modern cloud-native applications suffer from "Cold Start" latency on serverless platforms. This project demonstrates a **high-performance, low-footprint architecture** optimized for Google Cloud Run. By migrating from local scheduling to a cloud-native Azure DevOps environment, I achieved 100% environment consistency while maintaining production-grade reliability.

## 🏗️ System Architecture

The framework orchestrates infrastructure health through four specialized layers:

1.  **Ingestion Layer:** Multi-protocol support for periodic "Heartbeat" triggers via YAML-based `cron` schedules.
2.  **Validation Layer (The Gatekeeper):** A custom `pytest` suite that enforces configuration integrity and credential validation before execution.
3.  **Persistence Layer:** Secure management of sensitive relational storage and tokens using Azure DevOps Secret Variables.
4.  **Audit & Alerting:** A Slack-integrated monitoring system that detects performance anomalies and pushes real-time status notifications.

## 🔄 The Pipelines

* **Cloud Run Warmer:** Periodically pings the hosted portfolio to ensure the container remains warm and responsive for visitors, eliminating "Cold Start" latency.
* **Infrastructure Health Flow:** Dispatches detailed performance metrics and automated feedback (✅/❌) to a dedicated Slack channel for immediate transparency.
* **Strategic Risk Validator:** A specialized stage that acts as a pre-load gatekeeper, checking for environment drift and preventing "human error" or silent failures.

## 🛠️ Technical Stack

* **Cloud Provider:** Google Cloud Platform (Cloud Run)
* **Orchestration:** Azure DevOps (Azure Pipelines)
* **Automation:** Python 3.9 & YAML-based CI/CD
* **Testing & Monitoring:** Pytest, Slack API (Webhooks)

---

## 🚀 Installation & Setup

### Azure DevOps Configuration
1.  **Pipeline Import:** Create a new pipeline pointing to this repository.
2.  **Variables:** Define `SLACK_WEBHOOK` in your Azure Pipeline Library or Variable Group.
3.  **Deployment:** The `azure-pipelines.yml` handles environment setup, dependency installation, and execution.

### Local Development & Testing
```bash
# Create and activate virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run Validation Suite
python -m pytest tests/test_config.py

# Run Monitor Manually
python monitor_portfolio.py