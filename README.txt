Portfolio Monitor & Auto-Warmer
Technical implementations of automated infrastructure workflows designed for high-reliability cloud environments. This framework bridges the gap between Cold Start mitigation and Strategic Risk management through automated health checks and real-time alerting.

🎯 Project Philosophy
Most modern cloud-native applications suffer from "Cold Start" latency on serverless platforms. This project demonstrates a high-performance, low-footprint architecture optimized for Google Cloud Run. By migrating from local scheduling to a cloud-native Azure DevOps environment, I achieved 100% environment consistency while maintaining production-grade reliability.

🏗️ System Architecture
The framework orchestrates infrastructure health through four specialized layers:

Ingestion Layer: Periodic "Heartbeat" triggers via YAML-based cron schedules.

Validation Layer (The Gatekeeper): A custom pytest suite that enforces configuration integrity and credential validation before execution.

Persistence Layer: Secure management of sensitive tokens using Azure DevOps Secret Variables.

Audit & Alerting: A Slack-integrated monitoring system that detects performance anomalies and pushes real-time status notifications.

🔄 The Pipelines
Cloud Run Warmer: Periodically pings the hosted portfolio to ensure the container remains warm and responsive for visitors, eliminating latency.

Infrastructure Health Flow: Dispatches detailed performance metrics and automated feedback (✅/❌) to a dedicated Slack channel for immediate transparency.

Strategic Risk Validator: A specialized stage that acts as a pre-load gatekeeper, checking for environment drift and preventing "silent failures."

🛠️ Technical Stack
Cloud Provider: Google Cloud Platform (Cloud Run).

Orchestration: Azure DevOps (Azure Pipelines).

Automation: Python 3.9 & YAML-based CI/CD.

Monitoring: Slack API (Webhooks) & Pytest.

🚀 Installation & Setup
Azure DevOps Configuration
Pipeline Import: Create a new pipeline pointing to this repository.

Variables: Define SLACK_WEBHOOK in your Azure Pipeline Library.

Deployment: The azure-pipelines.yml handles environment setup and execution.

Local Development
Bash
# Install dependencies
pip install -r requirements.txt

# Run Validation Suite
python -m pytest tests/test_config.py

# Run Monitor Manually
python monitor_portfolio.py