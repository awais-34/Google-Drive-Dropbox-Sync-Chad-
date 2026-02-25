<div align="center">

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:0d0221,40:1a0533,100:0a0a1a&height=180&section=header&text=Crypto%20Vault%20Autosync&fontSize=46&fontColor=ffffff&fontAlignY=36&desc=Automated%20Google%20Drive%20%E2%86%92%20Dropbox%20Backup%20Pipeline&descAlignY=60&descSize=14&animation=fadeIn" />

<br/>

<img src="https://img.shields.io/badge/Status-Active%20%26%20Live-22c55e?style=for-the-badge&logo=circle&logoColor=white" />
&nbsp;
<img src="https://img.shields.io/badge/Trigger-Scheduled%20Cron-7c3aed?style=for-the-badge&logo=zapier&logoColor=white" />
&nbsp;
<img src="https://img.shields.io/badge/Source-Google%20Drive-34A853?style=for-the-badge&logo=google-drive&logoColor=white" />
&nbsp;
<img src="https://img.shields.io/badge/Destination-Dropbox-0061FE?style=for-the-badge&logo=dropbox&logoColor=white" />
&nbsp;
<img src="https://img.shields.io/badge/Built%20With-n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white" />

</div>

---

## 📌 What Is This?

**Crypto Vault Autosync** is a lightweight, high-reliability automated backup pipeline built in **n8n**. 

It runs on a scheduled interval to poll a specific *"Crypto"* folder in **Google Drive**, search for newly added or modified files, download them securely, and autonomously upload them to a mirrored `/Crypto/` vault in **Dropbox**. 

> Zero manual drag-and-drop. Redundant cold storage backups for critical crypto-related files and documents, operating fully autonomously.

---

## 🧭 System Overview

| Stage | Node / Tool | Role |
|:---|:---|:---|
| **1. Trigger** | Schedule Trigger | Wakes up the pipeline on a defined interval (e.g., daily/weekly). |
| **2. Poll Data** | Google Drive (Search) | Targets folder `112JjdO3...XWC72Ud` and lists all files inside. |
| **3. Batching** | Loop Over Items | Splits the file list into a batched queue to prevent memory limits. |
| **4. Ingestion** | Google Drive (Download) | Securely pulls the binary data of the file into n8n's temporary memory. |
| **5. Mirroring** | Dropbox (Upload) | Pushes the binary file to Dropbox at path `/Crypto/{filename}`. |

---

## 📸 Workflow Dashboard

<details open>
<summary><strong>👉 Storage Mirror Engine</strong></summary>

<br>
<img width="1471" height="536" alt="Screenshot 1" src="https://github.com/user-attachments/assets/ea46174e-451e-4871-8562-dd11319cfce5" />


<br>

</details>

---

## ⚡ Full System Architecture

<div align="center">

```mermaid
flowchart TD
    CRON(["⏰ Schedule Trigger\nRuns on set interval"]) --> SEARCH_GDRIVE

    SEARCH_GDRIVE["🔍 Google Drive\nSearch Folder: 'Crypto'\nReturns list of files"] --> BATCH_LOOP

    BATCH_LOOP{"🔁 Loop Over Items\nProcess 1 file at a time"}
    
    BATCH_LOOP -- "Next File" --> DOWNLOAD_GDRIVE
    
    DOWNLOAD_GDRIVE["📥 Google Drive\nDownload binary data\nby File ID"] --> BATCH_LOOP

    BATCH_LOOP -- "Upload Queue" --> UPLOAD_DROPBOX

    UPLOAD_DROPBOX["☁️ Dropbox\nUpload file binary\nPath: /Crypto/{{filename}}"] 

    style CRON fill:#302b63,color:#fff,stroke:#7c3aed
    style SEARCH_GDRIVE fill:#34A853,color:#fff,stroke:#26853f
    style BATCH_LOOP fill:#1e3a5f,color:#fff,stroke:#112540
    style DOWNLOAD_GDRIVE fill:#34A853,color:#fff,stroke:#26853f
    style UPLOAD_DROPBOX fill:#0061FE,color:#fff,stroke:#004bca
```

</div>

---

## 🛠️ Tech Stack

<div align="center">

| Tool | Role |
|:---|:---|
| ![n8n](https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white) | Workflow orchestration and binary data streaming |
| ![Google Drive](https://img.shields.io/badge/Google%20Drive-34A853?style=for-the-badge&logo=google-drive&logoColor=white) | Primary data source & active workspace |
| ![Dropbox](https://img.shields.io/badge/Dropbox-0061FE?style=for-the-badge&logo=dropbox&logoColor=white) | Redundant offline/cold storage mirror |

</div>

---

## 🚀 Setup Guide

### Prerequisites
- [ ] Active n8n environment
- [ ] Google Workspace / Developer App (OAuth2)
- [ ] Dropbox Developer App (OAuth2)

### Activation Steps
1. **Import Workflow:** Import `Google Drive: Poll & Download (Crypto).json` into n8n.
2. **Setup Credentials:** Connect your Google Drive OAuth2 and Dropbox OAuth2 credentials in the respective nodes.
3. **Verify Google Drive Folder ID:** 
   Ensure the `Search files and folders` node points to your correct Drive folder. (Currently hardcoded to `112JjdO3TyDrbvDNEHlTuz_DHFXWC72Ud`).
4. **Configure Interval:** Set the `Schedule Trigger` to your desired frequency (e.g., Every day at 2:00 AM).
5. **Activate:** Toggle the workflow to active.

> **Note on Binary Data:** This workflow streams binary data directly through n8n. Ensure your hosting environment has enough memory configured if you are syncing massive (1GB+) files.

---

<div align="center">

**Built by [Abdul Rehman](https://github.com/ar-rehman786)**

[![Gmail](https://img.shields.io/badge/Email-abdulrehmanhameed4321%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:abdulrehmanhameed4321@gmail.com)
&nbsp;
[![Slora AI](https://img.shields.io/badge/🚀_Slora_AI-sloraai.com-5D3EFF?style=for-the-badge)](https://www.sloraai.com/)
&nbsp;
[![GitHub](https://img.shields.io/badge/GitHub-ar--rehman786-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ar-rehman786)

</div>

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:0a0a1a,50:1a0533,100:0d0221&height=100&section=footer&animation=fadeIn" />
