# Portfolio Monitor & Auto-Warmer

An automated monitoring and orchestration pipeline designed to eliminate **"Cold Start"** latency on Google Cloud Run while providing real-time infrastructure alerts via Slack.

---

## 📋 Overview
This project serves a triple purpose:
1. **Cold Start Mitigation:** Periodically "pings" the Google Cloud Run hosted portfolio to ensure the container remains warm and responsive.
2. **Infrastructure Auditing:** Automatically checks the health of the live URL and logs performance metrics.
3. **Real-time Alerting:** Dispatches status reports to a dedicated Slack channel using a custom Slack App.

## 🛠️ Technical Stack
* **Language:** Python 3.x
* **Cloud Provider:** Google Cloud Platform (Cloud Run)
* **Orchestration:** **Azure DevOps (Azure Pipelines)**
* **Automation:** YAML-based CI/CD Pipelines
* **Communication:** Slack API (WebClient)
* **Environment Management:** Docker & Python Virtual Environments

---

## ⚙️ Architecture & Automation

### 1. Cloud-Native Orchestration (Azure DevOps)
The project has migrated from local Windows Task Scheduling to **Azure Pipelines**. This move ensures environment consistency and higher reliability:
* **Scheduled Triggers:** The heartbeat is controlled via `cron` schedules within `azure-pipelines.yml`, ensuring the Cloud Run instance remains active without manual intervention.
* **Automated Workflow:** The pipeline automatically handles dependency installation, environment setup, and script execution in a clean, containerized agent.
* **Secret Management:** Sensitive tokens and URLs are managed via Azure DevOps Variable Groups rather than local files.

### 2. The Slack Integration
The system integrates with the Slack API to provide transparency into the pipeline's health.
* **Security Model:** Uses a "Need-to-Know" protocol where the Bot User must be explicitly invited to the target channel to grant posting permissions.
* **Automated Feedback:** Provides immediate visual confirmation (e.g., ✅ status) upon successful pings or failure alerts for immediate troubleshooting.

---

## 🚀 Installation & Setup

### Azure DevOps Configuration
1. **Pipeline Import:** Create a new pipeline in Azure DevOps pointing to this repository.
2. **Variables:** Define the following secret variables in your Azure Pipeline Library:
   * `SLACK_BOT_TOKEN`: Your Slack App OAuth token.
   * `TARGET_URL`: Your portfolio's live URL.
3. **Trigger:** Ensure the `schedules` block in `azure-pipelines.yml` is configured for your desired frequency.

### Local Development
```bash
# Create and activate virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt