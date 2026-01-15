# ai-retention-bot

# 📸 AI-Powered Customer Retention Engine

> **A smart, state-aware automation system designed to optimize post-event engagement, prevent coupon fraud, and route high-value leads.**

![n8n](https://img.shields.io/badge/Orchestration-n8n-orange) ![AI](https://img.shields.io/badge/AI-Llama%203.1-blue) ![Database](https://img.shields.io/badge/Database-Google%20Sheets-green) ![Messaging](https://img.shields.io/badge/Messaging-Twilio-red)

## 📖 Project Overview
For **Hatk**, a photobooth startup, generic "Thank You" messages were resulting in low engagement. I engineered an intelligent retention workflow that personalizes user communication, respects user time zones, and segments high-value corporate leads from general consumers.

The system moves beyond simple automation to include **A/B Testing**, **Database Validation**, and **Microservices Architecture** to ensure scalability and data integrity.

---

## 🏗️ Architecture & Logic
The system is decoupled into two primary workflows to ensure non-blocking execution.

### 1. The Main Engine (Sender & Router)
This workflow handles the customer lifecycle from the moment a photo is taken.
* **Segmentation:** Filters users by email domain. `Gmail/Yahoo` users enter the Consumer Flow; `Corporate` domains enter the VIP Flow.
* **A/B Testing:** Splits Consumer traffic 50/50 between "AI-Generated Humor" and "Standard Messaging" to measure engagement rates.
* **Generative AI:** Uses **Llama 3 (via Groq)** to generate unique, context-aware puns based on the guest's name.
* **Time-Intelligence:** Checks the current time before sending follow-ups. If it is night (9 PM - 9 AM), the bot "sleeps" to protect Brand UX.

![Workflow Architecture](![Screenshot_16-1-2026_11435_arjunvvv app n8n cloud](https://github.com/user-attachments/assets/4bf2ff34-19ca-42b2-9b92-0c3006030023)
)
*(Fig 1: The Main Lifecycle Workflow showing Segmentation and Time Logic)*

### 2. The Listener (Verification Service)
This microservice listens for incoming SMS replies ("DONE") to unlock discount codes.
* **Anti-Fraud Validation:** It does not blindly send coupons. It performs a **Database Lookup** in Google Sheets to verify the user actually submitted the feedback form.
* **Data Cleaning:** Normalizes phone number formats (removing `+91`) to ensure accurate database matching.

![Verification Logic](![Screenshot_16-1-2026_1115_arjunvvv app n8n cloud](https://github.com/user-attachments/assets/ddee41b0-412f-40e1-8166-f00e60a1f226)
)
*(Fig 2: The Verification Logic with Database Lookup)*

---

## 🚀 Key Features (PM Perspective)

| Feature | Business Value | Technical Implementation |
| :--- | :--- | :--- |
| **Microservices** | Zero-latency alerts for Sales Team. | Decoupled "VIP Handler" from the main AI workflow using asynchronous triggers. |
| **Sales CRM** | Prevents missed high-ticket leads. | Automated logging of corporate emails into a dedicated "VIP_Leads" dashboard. |
| **A/B Experiment** | Data-driven content strategy. | Randomizer node splits traffic; Cohorts logged to DB for analysis. |
| **Fraud Guard** | Protects revenue/margins. | Cross-referencing inbound SMS with Form Database before reward release. |

---

## 🛠️ Tech Stack
* **n8n:** Workflow orchestration and logic handling.
* **Groq API (Llama 3.1):** High-speed, low-cost LLM inference for personalization.
* **Google Sheets:** Acts as the CRM (Customer Relationship Management) and Validation Database.
* **Twilio:** SMS gateway for bi-directional communication.

---

## ⚙️ How to Run
This repository contains the JSON source code for the automation.

1.  **Install n8n:** Run n8n locally (`npm run n8n`) or sign up for n8n Cloud.
2.  **Import Workflow:**
    * Download `workflow.json` from this repo.
    * In n8n, go to **Menu** > **Import**.
3.  **Configure Credentials:**
    * Add your **Twilio** (SID & Auth Token).
    * Add your **Groq API Key**.
    * Connect your **Google Google Account**.
4.  **Activate:** Toggle the workflow to `Active`.

---

## 👤 Author
**Arjun Varshney**
*Product Management & Growth Engineering*

[LinkedIn](https://www.linkedin.com/in/arjun-varshney-178b042a6/) | [Email](mailto:arjunvarshney13@gmail.com)
