# My Office Intern

A governed AI email workflow system designed to explore safe automation, validation, and human-in-the-loop operations.

The system combines AI-assisted draft generation with validation, governance, workflow routing, and human review controls to support safer email operations.

## Features

Current capabilities include:

- Reading customer emails from Gmail in read-only mode
- Classifying incoming emails
- Generating AI-assisted draft responses
- Validating drafts against operational rules
- Routing emails through governed workflows
- Supporting human review and approval workflows
- Determining automation eligibility
- Tracking operational metrics and outcomes
- Maintaining workflow state and audit history
- Managing email queues for testing and review

---

## Architecture

```text
Customer Email
        ↓
 Classification
(What type of email is this?)
        ↓
 Draft Generation
(Create a proposed response)
        ↓
 Validation
(Did the draft violate rules?)
        ↓
 Governance
(Is automation allowed?)
        ↓
 ┌───────────────┴───────────────┐
 ↓                               ↓

Human Review                 Auto Ready
(Person approves)            (Eligible for automation)
        ↓                               ↓
       Sent                           Sent
```
## Tech Stack

- Python backend
- Vanilla JavaScript frontend
- SQLite persistence
- Gmail IMAP (read-only)
- Ollama for local AI inference

## Gmail setup

1. Enable 2-Step Verification on your Google account.
2. Create a Gmail app password for this project.
3. Copy `.env.example` to `.env`.
4. Fill in your credentials:

```bash
GMAIL_ADDRESS=youraddress@gmail.com
GMAIL_APP_PASSWORD=your-app-password
```

Do not commit `.env`. It is ignored by Git.

---

## Run the system

### 1. Start backend (Terminal 1)

```bash
python3 backend.py
```

It starts at:

```text
http://127.0.0.1:8000
```

---

### 2. Start frontend server (Terminal 2)

```bash
python3 -m http.server 5500
```

---

### 3. Open in browser

```text
http://127.0.0.1:5500/index.html
```

## API

Check that the backend is running:

```bash
curl http://127.0.0.1:8000/health
```

Read unread email previews:

```bash
curl http://127.0.0.1:8000/unread-subjects
```

Optionally limit the number of subjects:

```bash
curl "http://127.0.0.1:8000/unread-subjects?limit=10"
```

Example response:

```json
{
  "emails": [
    {
      "id": "42",
      "sender": "Alex Lee <alex@example.com>",
      "subject": "Question about the onboarding checklist",
      "date": "Mon, 27 Apr 2026 10:15:00 -0500",
      "dateIso": "2026-04-27T15:15:00+00:00",
      "preview": "Could you review the onboarding checklist before Friday?"
    }
  ]
}
```

## Use the frontend

Open `index.html` in a browser after starting the backend. Click **Refresh Inbox** to load unread emails from Gmail, then select one before generating a draft.
