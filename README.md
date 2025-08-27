# VistaOps

## 📘 Laundry Notifications MVP

**VistaOps** is a lightweight, AWS-native tool to help **Mental Health Counselors (MHCs)** and nursing staff track patient laundry across shift changes. The MVP provides a dead-simple flow to **log items, update statuses, and send shift-ready reminders** — reducing lost/late laundry and improving handoff communication.

---

## 🚀 Features (MVP)

- **Create laundry item** (first name + unit)
- **Update status**: `washing → drying → ready → returned`
- **Mobile-first view** with big Ready / Returned buttons
- **24-hour auto-purge** of items (privacy + simplicity)
- **Shared passcode auth** (MVP only)
- **Optional SMS alerts** when laundry is ready (Twilio, feature-flagged)
- **Handoff digest** for lead nurse (open items grouped by unit)

---

## 🛠️ Tech Stack

**Frontend**

- Static page in `/web/` (HTML + Tailwind CDN + vanilla JS)
- QR code generation via open-source library (`QRCode.js`)
- Hosted on **AWS S3 + CloudFront** (with optional Route 53 domain)

**Backend (next phase)**

- Runtime: **Node.js + TypeScript**
- Framework: **Fastify (or Express)** with **Zod** validation
- Database: **DynamoDB** with TTL for 24h expiry
- API Gateway (HTTP API) → Lambda → DynamoDB
- EventBridge for AM/PM digest jobs
- SMS: Twilio (dry-run by default)

**Infra**

- AWS S3 (static site)
- AWS CloudFront (CDN + HTTPS via ACM)
- AWS Route 53 (custom domain, e.g., `vistaops.tech`)

---

## 📐 Architecture (MVP view)

```
MHC → Mobile browser → S3 + CloudFront (static UI)
                         |
                         V
                API Gateway → Lambda (Node/TS)
                              |
                              V
                          DynamoDB (TTL purge)
```

---

## 📲 Example Flow

1. MHC logs laundry item with **first name + unit**
2. Item status moves through `washing → drying → ready → returned`
3. On **Ready**, SMS alert is sent to on-duty roster (if enabled)
4. Items auto-purge after 24h; lead gets digest summary

---

## 🔒 Privacy & Compliance

- Only **first name** is stored (no PHI beyond that)
- Auto-purge after 24h using DynamoDB TTL
- HTTPS enforced via CloudFront + ACM
- Logs contain metadata only (no request bodies)

---

## 📊 Metrics (future)

- Avg. time from started → ready
- Count of expired items (>24h not returned)
- SMS sends per unit per day

---

## 🧭 Roadmap

- ✅ Day 1: Repo setup + static `/web/index.html` deployed via S3/CloudFront
- ⏳ Backend: API GW + Lambda + DynamoDB schema + Twilio integration
- ⏳ Self check-in via SMS keywords (`ON 3A` / `OFF 3A`)
- ⏳ React SPA (optional) when flows expand (filters, roles, toasts)
- ⏳ Aurora Serverless Postgres for reporting / analytics

---

## ⚡ Quick Start (Local Dev)

```bash
# clone repo
git clone https://github.com/<your-handle>/VistaOps.git
cd VistaOps

# preview static site
cd web
open index.html   # or use 'npx http-server' for localhost preview
```

---

## 🌍 Deploy (Day 1 static site)

1. Create an S3 bucket (unique name, e.g. `vistaops-demo`)
2. Enable **Static Website Hosting** → set `index.html`
3. Upload files from `/web/`
4. (Optional) Put CloudFront in front for HTTPS
5. (Optional) Route 53 domain alias → CloudFront

---

## 👥 Contributors

- **Owner:** Sayeed Joseph
- Contributions welcome once MVP API is live

---
