# System Health Metric Analyser Platform

> **An end-to-end AI-powered system health monitoring solution combining local telemetry, cloud analytics, and agentic diagnostics.**

---

## 📖 Project Overview

**System Health Metric Analyser** is a distributed platform designed to move beyond simple resource monitoring. Instead of just showing you a CPU graph, it uses **Generative AI** and **Machine Learning** to explain *why* your system is behaving the way it is.

The ecosystem is split into two specialized applications:

1.  **Desktop Agent (PyQt5):** A local "sensor" that runs on the user's machine. It collects low-level hardware metrics (CPU, RAM, Thermals) via `psutil`, runs local anomaly detection models, and securely uploads encrypted reports to the cloud.
2.  **Web Dashboard (Streamlit):** A cloud-native "command center." It visualizes historical data and hosts an **Agentic AI Chatbot** (powered by RAG) that acts as a virtual Systems Administrator, diagnosing issues based on the uploaded telemetry.

---

## 📂 Repository Structure

This repository is a **Monorepo Aggregation**. It uses **Git Submodules** to bundle the independent client and server repositories.

```text
System-Health-AI/
├── desktop-agent/       # [Submodule] The local PyQt5 Client App
│   ├── main.py
│   ├── resources/
│   └── requirements.txt
│
├── web-dashboard/       # [Submodule] The Streamlit Cloud App
│   ├── app.py
│   ├── pages/
│   └── requirements.txt
│
└── README.md            # You are here
```

---

## ⚡️ Installation (CRITICAL)
Because this repository uses Submodules, a standard git clone will result in empty folders. You must use the recursive flag.

Option A: Fresh Clone (Recommended)
Use this command to download the parent repo and both sub-projects simultaneously:

```Bash
git clone --recurse-submodules [https://github.com/YourUsername/System-Health-AI-Platform.git](https://github.com/YourUsername/System-Health-AI-Platform.git)
```

Option B: If you already cloned normally
If you cloned the repo and the folders are empty, run this command to fetch the submodules:

```Bash
git submodule update --init --recursive
```

## 🛠️ Configuration & Setup
Since the system relies on a unified cloud backend, both applications need credentials to talk to Supabase and Google OAuth.

1. Environment Variables
Create a .env file (for Desktop) or .streamlit/secrets.toml (for Web) containing your credentials:
Ini, TOML

# Example Configuration
```SUPABASE_URL="[https://your-project.supabase.co](https://your-project.supabase.co)"
SUPABASE_KEY="your-anon-key"
GOOGLE_CLIENT_ID="your-oauth-client-id"
CHROMA_DB_PATH="./chroma_db"
```

## 🚀 Running the Applications
You will need to run the Desktop Agent to generate data, and the Web Dashboard to view it. It is recommended to run these in separate terminal windows.

A. Start the Desktop Agent (Data Producer)
```Bash
cd desktop-agent

# 1. Create a virtual environment (Recommended)
python -m venv venv
# Windows: venv\Scripts\activate | Mac/Linux: source venv/bin/activate

# 2. Install Dependencies
pip install -r requirements.txt

# 3. Run the App
python main.py
```

B. Start the Web Dashboard (Data Consumer)
```Bash
cd ../web-dashboard

# 1. Create a virtual environment
python -m venv venv
# Windows: venv\Scripts\activate | Mac/Linux: source venv/bin/activate

# 2. Install Dependencies
pip install -r requirements.txt

# 3. Launch Streamlit
streamlit run app.py
```

## 🏗 Architecture
```Code snippet
graph TD
    User((User))
    
    subgraph Local_Machine [Local Machine]
        Desktop[PyQt5 Agent]
        Metric[psutil Telemetry]
        Desktop --> Metric
    end

    subgraph Cloud [Cloud Infrastructure]
        Supabase[(Supabase DB)]
        Chroma[(Chroma Vector DB)]
        Web[Streamlit Dashboard]
        AI[Agentic AI]
    end

    Desktop -- Secure Upload --> Supabase
    Web -- Read History --> Supabase
    Web -- Context Retrieval --> Chroma
    AI -- Diagnostics --> Web
    User -- View --> Web
```
