#  AI Lead Management System

An end-to-end automated lead management system built with **n8n**, **Odoo CRM**, **OpenAI GPT-4o Mini**, **Twilio WhatsApp**, and **Gmail** — designed to score,
route, and nurture leads automatically.

---

##  Live Demo

- **Lead Form:** https://odoo-lead-submittionform.netlify.app/
- **CRM Dashboard:** Odoo 17 Community (Self-hosted)
- **Automation Engine:** n8n (Self-hosted)

---

##  System Architecture

```
Lead Form (HTML)
      ↓
Webhook (n8n) — Auth Protected
      ↓
Rate Limit & Spam Check
      ↓
Duplicate Email Check (Odoo)
      ↓
Data Validation & Formatting
      ↓
AI Scoring (GPT-4o Mini)
      ↓
Smart Assignment (Senior/Junior Rep)
      ↓
Odoo CRM — Lead Created
      ↓
┌─────────────────────┐
│  HOT / WARM / COLD  │
└─────────────────────┘
      ↓
WhatsApp Alert (Twilio) + Email to Rep
      ↓
Confirmation Email to Customer
      ↓
14-Day Nurture Sequence (4 Emails)
   → Day 3 → Day 7 → Day 14
   → Smart Stop if Won/Lost in Odoo
```

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🤖 AI Lead Scoring | GPT-4o Mini scores leads 0-100 based on budget, timeline, requirement, company size & decision maker |
| 🎯 Smart Assignment | Score ≥70 → Senior Rep \| Score <70 → Junior Rep |
| 🔥 HOT/WARM/COLD Routing | Single branch routing — no duplicate notifications |
| 📱 WhatsApp Alerts | Twilio sends instant WhatsApp to assigned sales rep |
| 📧 Email Automation | Rep notification + Customer confirmation + 4-email nurture sequence |
| 🛑 Smart Stop | Checks Odoo CRM before every follow-up — stops if lead is Won or Lost |
| 🔒 Spam Protection | Rate limiting & spam detection on webhook |
| ✅ Duplicate Prevention | Blocks duplicate leads by email via Odoo check |
| ⚠️ Error Handling | Admin alert email on any workflow failure |

---

## 🧠 AI Scoring Logic

```
Total Score: 0–100

Budget (0–25 pts):
  Rs. 500k+  → 25 pts
  Rs. 100k+  → 20 pts
  Rs. 50k+   → 15 pts
  Rs. 10k+   → 10 pts
  Below      →  5 pts

Timeline Urgency (0–25 pts):
  1 day  → 25 pts
  7 days → 20 pts
  14 days→ 15 pts
  30 days→ 10 pts
  90 days→  5 pts

Requirement Detail (0–20 pts):
  Specific → 20 pts
  Vague    → 10 pts

Company Size (0–15 pts):
  Large  → 15 pts
  Medium → 10 pts
  Small  →  5 pts

Decision Maker (0–15 pts):
  Yes → 15 pts
  No  →  0 pts

Categories:
  70–100 = 🔥 HOT  → Senior Rep → Contact within 1 hour
  50–69  = 🟡 WARM → Junior Rep → Contact within 24 hours
  0–49   = ❄️ COLD → Email Nurture → Automated sequence
```

---

## 🗺️ Nurture Email Sequence

```
Day 0  → Confirmation Email ✅
Day 3  → Check Odoo Status → Follow-up Email
Day 7  → Check Odoo Status → Value-Add Email
Day 14 → Check Odoo Status → Final Email (Free Consultation)

Smart Stop: If lead marked Won (100% probability) or Lost (archived)
            → Email sequence stops automatically
```

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **n8n** | Workflow automation engine (self-hosted) |
| **Odoo 17** | CRM & lead management (self-hosted) |
| **OpenAI GPT-4o Mini** | AI lead scoring |
| **Twilio** | WhatsApp notifications |
| **Gmail API** | Email notifications & nurture sequence |
| **Google Cloud VM** | Hosting (Debian 12, e2-medium) |
| **HTML/CSS/JS** | Lead capture form |
| **Netlify** | Form hosting |

---

## 📁 Project Structure

```
├── lead_management_FINAL_FIXED.json  # n8n workflow (import this)
├── lead_form_final.html              # Lead capture form
├── production_nodes.json             # Rate limiting & spam check nodes
└── README.md                         # This file
```

---

## ⚙️ Setup Guide

### 1. Prerequisites
- n8n instance (cloud or self-hosted)
- Odoo 17 instance
- OpenAI API key
- Twilio account
- Gmail OAuth2 credentials

### 2. Import Workflow
1. Open n8n
2. Go to **Workflows → Import**
3. Upload `lead_management_FINAL_FIXED.json`
4. Update credentials (OpenAI, Odoo, Gmail, Twilio)

### 3. Configure Odoo
- Create 2 sales users (Senior & Junior rep)
- Note their user IDs
- Update IDs in **Code - Parse AI Score** node

### 4. Update Webhook Auth
In `lead_form_final.html`:
```javascript
'X-Auth-Token': 'your-secret-token'
```
Match this in n8n **Header Auth** credential.

### 5. Activate Workflow
Toggle **Active** in n8n — system is live! 🚀

---

## 📊 Results

- ✅ Leads scored and routed in **< 5 seconds**
- ✅ HOT leads notified via WhatsApp **instantly**
- ✅ Zero duplicate leads in CRM
- ✅ Automated follow-up for 14 days
- ✅ Smart stop prevents emails to closed deals

---
