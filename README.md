
<h1 align="center">
  <a href="https://github.com/CommunityOfCoders/Inheritance2k25">
    CoC Inheritance 2025
  </a>
  <br>
  System Health Metrics Analyser :  
</h1>

<div align="center">
By MAT(N)
</div>
<hr>

<details>
<summary>Table of Contents</summary>

- [Description](#description)
- [Links](#links)
- [Tech Stack](#tech-stack)
- [Progress](#progress)
- [Future Scope](#future-scope)
- [Applications](#applications)
- [Project Setup](#project-setup)
- [Team Members](#team-members)
- [Mentors](#mentors)

</details>
<a name="description"></a>

## 📝 Description

System Health AI is a **full-stack intelligent diagnostics platform** designed to analyze, understand, and predict system behavior using **machine learning, generative AI, and autonomous agents.**
<br><br>
This project bridges that gap by combining **local telemetry analysis, cloud-based intelligence,** and **AI-driven reasoning** to deliver **actionable system insights** instead of raw numbers.


<a name="links"></a>

## 🔗 Links

- [GitHub Repository](https://github.com/MohdHedayati/System-Health-Metric-Analyser)
- [Demo Video](https://drive.google.com/file/d/1_DHHsarQ92n83EXDuWiwfLH7hvWbbe-V/view?usp=sharing)
- [Screenshots Folder](https://drive.google.com/drive/folders/1-brArJMhcJ39OdvRuXasdtj291JhqGjT?usp=drive_link)
- [Hosted Website](https://once-1296-web-app-for-system-health-metrics-analyse-main-5evupf.streamlit.app/)

<a name="tech-stack"></a>

## 🤖 Tech-Stack
1. Web App
* Streamlit (Python)
* chromadb (For RAG)
2. Desktop App
* PyQt5
* psutils for metric collection
* torch , onnxscript, onnxruntime for ML
3. Database
* Supabase Postgresql
* Typescript (Supabase Edge Function)
### 🏗️ System Architecture

```mermaid
graph LR
    User --> Login["Login (Google OAuth)"]

    Login --> WebApp["Web App"]
    WebApp --> Reports["Supabase: User Reports"]
    Reports --> Visuals["Text Report & Analytical Visualization"]

    WebApp --> NewChat["New Chat"]
    NewChat --> ChatQuery["Send Query"]
    ChatQuery --> RAG["RAG (ChromaDB)"]
    RAG --> LLM["LLM"]
    LLM --> Response["Response"]
    Response --> StoreChat["Store Chat & Summary"]
    StoreChat --> Supabase[(Supabase)]

    Supabase --> FetchOldChat["Fetch Old Chat"]
    FetchOldChat --> NewChat

    Login --> DesktopApp["Desktop App"]
    DesktopApp --> Monitor["Monitor System"]
    Monitor --> DataCollected["Data Collected"]
    DataCollected --> MLModel["ML Model"]
    MLModel --> CleanedSummary["Cleaned Summary"]
    CleanedSummary --> UploadData["Upload Raw + Cleaned Data + Metadata"]
    UploadData --> Supabase

    Login --> Logout["Log Out"]
			  
						   					  
```

### Front-end
* [Streamlit](https://streamlit.io/) --> Blazing Fast Web UI with Easy Deployment and Smooth Visualisation of Reports
* [PyQt5](https://doc.qt.io/archives/qtforpython-5/) --> Minimal Desktop App, Single executable file, with easy execution and Simple Design
### Back-end
* Google OAuth --> Smooth Login and Sign Up
* Loading user's chats and reports --> postgresql type queries via supabase module in python.
* [render](https://render.com):
	* onnx Models hosted for Windows Desktop App
### Database 
* [Supabase](https://supabase.com/):
	* Store chats and user details, alongside System Reports
	* Edge function and RLS policies to maintain strict schema of System Reports
### AIML 
* Multiple LLMs like LLama3b, mistral, etc. *(via Groq)* for specific operations *(responding, summarising,etc)*
* Models trained with torch based neural networks *(torch.nn)* , using **Adam Optimiser, ReLU Activation Function** and **Cross Entropy Loss.**
* **pth** models trained by torch converted to **onnx** for making application lightweight.

<a name="progress"></a>

## 📈 Progress

### Fully Implemented Features

* **CRUD Based Chat System**: Chats are added, deleted and updated smoothly via Supabase and streamlit.
* **Collecting System Metrics via psutils**: Standard metrics like memory, cpu, temps, disk usage, etc. are appropriately measured
* **Functional Vector DB for RAG**: Vector DB is suitably chunkized, and stored with metadata to ensure pinpoint and extremly accurate answers with docs fetched being almost always relevant to the query of user

---

### Partially Implemented Features / Work in Progress

* **Continous Integration between chatbot and local app**: Chatbot should also analyse reports on own: backend needs to be tweaked a bit more to make this a reality.
* **Collecting Binary LOgs and applying more advanced ML models**: ML part can be refined more to analyse binary logs as well, which can help catch even highly professional cybersecurity attacks.

<a name="future-scope"></a>

## 🔮 Future Scope

* We can host much heavier models with Cloud Computing Services.
* RAG based Vector DB and desktop app can be expanded to more OS beyond the current 3.
* Multiple Authentication modes can be implemented instead of just Google OAuth.

<a name="applications"></a>

## 💸 Applications

1. **System Monitoring and Safety** - Malware classification and anomalous behavior of PC based on memory, CPU and temperature data.
2. **Smart Assistant For PC Software fixes** - Acting as a laser focused, non-hallucinating assistant to resolve unexplained and erratic behavior of user's PCs (For eg freezing of Windows keyboard due to an accidental key shortcut).

<a name="project-setup"></a>

## 🛠 Project Setup

If you wish to run the source code or contribute, follow these steps.

## 🌐 Web App

#### 1. Installation
```bash
# Clone the Web App branch
git clone https://github.com/Once-1296/Web_App_For_System_Health_Metrics_Analyser.git

# Create Virtual Environment
python -m venv venv
# Activate: source venv/bin/activate (Mac/Linux) or .\venv\Scripts\activate (Windows)

# Install Dependencies
pip install -r requirements.txt

# Run the Application
streamlit run app.py
```

#### 2. Configuration (secrets.toml)
Streamlit manages secrets differently than the desktop app. You must create a file at .streamlit/secrets.toml.

```File Structure:

.streamlit/
└── secrets.toml
app.py
Content of .streamlit/secrets.toml:

Ini, TOML
[supabase]
url = "[https://your-project.supabase.co](https://your-project.supabase.co)"
key = "your-anon-key"

[google_auth]
client_id = "your-google-client-id"
client_secret = "your-google-client-secret"
```

## 🖥️ Desktop App

#### 1. Installation
```bash
# Clone the Windows branch
git clone https://github.com/MohdHedayati/Local-app---system-health-metric-analyzer.git

# Create Virtual Environment (Verified on Python 3.12.0)
python -m venv venv 
# Activate venv: .\venv\Scripts\activate

# Install Dependencies
pip install -r requirements.txt

# Run the Application
cd PyQt5
python app.py
```

#### 2. Configuration Secrets (Crucial)
The application will not start without API credentials. You must create a data folder inside the PyQt5 directory and add the following two JSON files:

```File Structure:

Plaintext
PyQt5/
├── app.py
├── data/
│   ├── client_secrets.json
│   └── supabase_secrets.json
```

#### A. PyQt5/data/client_secrets.json (Google OAuth)
Get this from your Google Cloud Console. It should look like this:

```JSON
{
  "installed": {
    "client_id": "35809.....apps.googleusercontent.com",
    "project_id": "sodium-primer-48...",
    "auth_uri": "[https://accounts.google.com/o/oauth2/auth](https://accounts.google.com/o/oauth2/auth)",
    "token_uri": "[https://oauth2.googleapis.com/token](https://oauth2.googleapis.com/token)",
    "auth_provider_x509_cert_url": "[https://www.googleapis.com/oauth2/v1/certs](https://www.googleapis.com/oauth2/v1/certs)",
    "client_secret": "GOCS...",
    "redirect_uris": ["http://localhost"]
  }
}
```

#### B. PyQt5/data/supabase_secrets.json (Database)
Get this from your Supabase Project Settings.

```JSON
{
    "PROJECT_URL": "[https://bozt....supabase.co](https://bozt....supabase.co)",
    "service_role_key": "eyJhbG....."
}
```

<a name="team-members"></a>

## 👨‍💻 Team Members

* **Awwab Wadekar**: [Once-1296](https://github.com/Once-1296)
* **Mohammed Hedayati**: [MohdHedayati](https://github.com/MohdHedayati)
* **Taha Valiji**: [tmvalijib24](https://github.com/tmvalijib24)
* **Nathan Dsouza**: [AsparkArcane](https://github.com/AsparkArcane)


<a name="mentors"></a>

## 👨‍🏫 Mentors

* **Amal Verma**: [amal-verma](https://www.linkedin.com/in/amal-verma/)
* **Prathamesh Sankhe**: [PMS61](https://github.com/PMS61) 
