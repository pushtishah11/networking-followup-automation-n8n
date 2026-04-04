# 🤝 Networking Follow-Up Email Automation

An n8n workflow that automatically generates personalized follow-up emails after networking meetings using Google Gemini, then logs the contact to Google Sheets and saves a Gmail draft — ready to review and send.

---

## ✨ What It Does

1. **Form submission** — Fill out a simple form with contact details after a networking meeting
2. **AI email generation** — Google Gemini writes a warm, personalized follow-up email based on the context
3. **Logs to Google Sheets** — Contact info + generated email are saved for your records
4. **Creates a Gmail draft** — The email lands in your drafts, ready to review and send with one click

---

## 🔁 Workflow Overview

```
On Form Submission
       │
       ├──────────────────┐
       │                  │
  Basic LLM Chain      (raw form data)
  (Google Gemini)         │
  Structured Output       │
  Parser                  │
       │                  │
       └────── Merge ─────┘
                  │
        ┌─────────┴──────────┐
        │                    │
  Append Row           Create Gmail
  (Google Sheets)        Draft
```

---

## 📋 Form Fields

| Field | Description |
|---|---|
| Name of Contact | Full name of the person you met |
| Company of Contact | Where they work |
| Role of Contact | Their job title |
| Where We Met | Event, platform, or context |
| What We Talked About | Key topics from the conversation |
| Contact Email | Their email address |

---

## 🛠️ Setup

### Prerequisites
- [n8n](https://n8n.io/) (self-hosted or cloud)
- Google account with Gmail + Google Sheets access
- Google Gemini API key

### Steps

1. **Import the workflow**
   - Download `workflow.json` from this repo
   - In n8n: click the menu (⋯) → *Import from file*

2. **Connect credentials**
   - **Google Gemini**: Add your API key under *Credentials → Google Gemini*
   - **Gmail**: Connect via OAuth in the Gmail node
   - **Google Sheets**: Connect via OAuth and point to your target spreadsheet

3. **Configure Google Sheets**
   - Create a sheet with columns matching the form fields + an `Email Draft` column
   - Update the *Append Row* node to point to your sheet

4. **Activate the workflow**
   - Toggle the workflow to **Active** in the top-right corner
   - Use the form trigger URL to submit entries

---

## 🧠 Prompt Design

The LLM is instructed to write emails that are:
- Warm and genuine, not templated or salesy
- Grounded in the specific context of where you met and what you discussed
- Ending with a low-pressure next step (coffee chat, resource share, etc.)

A **Structured Output Parser** ensures the response is split cleanly into `subject` and `body` fields for easy routing into Gmail and Sheets.

---

## 📸 Screenshots

> *(Add your own screenshots here)*
> - Workflow graph
> - Example form input
> - Example generated email

---

## 🚀 Potential Extensions

- Add a follow-up reminder (e.g., ping you after 1 week if no reply)
- Connect to LinkedIn via Phantombuster to auto-attach profile context
- Add a Slack notification when a draft is created
- Build a contact tracker dashboard from the Sheets data

---

## 🧰 Tech Stack

- [n8n](https://n8n.io/) — workflow automation
- [Google Gemini](https://deepmind.google/technologies/gemini/) — LLM for email generation
- Gmail API — draft creation
- Google Sheets API — contact logging

---

## 📄 License

MIT — feel free to use, fork, and build on this.
