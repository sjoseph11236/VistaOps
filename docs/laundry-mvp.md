# VistaOps

## Laundry Notifications MVP — Design Doc (Living)

### 1) Problem statement

MHC staff need a dead-simple way to log and track patient laundry across shift changes and receive timely “ready” notifications, reducing losses and late returns within a 24-hour window.

---

### 2) Primary users & usage moments

- **Users:** Mental Health Counselors (MHCs) and the lead nurse.
- **When:** during laundry collection, wash, dry, ready, return, and shift handoffs.
- **Goal:** shortest path = mobile form with first name + unit, plus an open list.

---

### 3) MVP scope

**In:**

- Create laundry item (first name + unit).
- Update status: washing → drying → ready → returned.
- Open list view with big “Ready/Returned” buttons.
- Shared passcode auth (MVP only).
- 24h expiry of items.

**Out (for now):**

- Photos, room mapping, SSO, deep WFM integrations.

---

### 4) Workflow (happy path)

1. MHC logs item (first name + unit).
2. Item progresses through statuses.
3. On “ready,” send SMS to on-duty staff (dry-run for MVP).
4. Handoff: lead nurse sees grouped open items per unit.

---

### 5) Privacy & compliance

- Identifier: **first name only**.
- Retention: purge items after 24h.
- Storage: DynamoDB with TTL.
- Access: shared passcode header.

---

### 6) Notifications

- Channel: SMS (Twilio, feature-flagged).
- Message:
  - Ready → `Laundry ready — <FirstName> — <Unit>`
  - Handoff digest → `Handoff — Open: <Name/status>`
- Anti-spam: only 1 “ready” SMS per item.

---

### 7) Who is on duty

- MVP: CSV roster upload (`unit, phone`).
- Fallback: if no roster entry, skip SMS but keep open list.

---

### 8) Data model (minimal)

- `LaundryItem { id, unit, firstName, status, startedAt, updatedAt, readyAt?, returnedAt? }`
- `ActiveRoster { unit, phone, addedAt, expiresAt }`

---

### 9) API surface (MVP)

- `POST /laundry` — create item.
- `PATCH /laundry/:id/status` — update status.
- `GET /laundry?unit=…&open=true` — list open items.
- `POST /roster/upload` — add roster.

---

### 10) UI surfaces

- Mobile-first page with:
  - Create item form (first name + unit).
  - Open list with big buttons.
  - QR generator for quick check-in.

---

### 11) Error & edge cases

- Duplicate names → append timestamp.
- No service → fall back to open list.
- Night rollover → open items persist until TTL purge.

---

### 12) Security

- Shared passcode auth.
- No PHI beyond first name.
- Log only metadata, not bodies.

---

### 13) Metrics

- Time from started → ready.
- Count of expired (not returned in 24h).
- SMS sends per day per unit.

---

### 14) Pilot & rollout

- Pilot unit: 3A.
- Digest times: 07:00 and 19:00.
- Training: one-pager with QR + passcode.

---

### 15) Risks & mitigations

- **Adoption:** keep flows 2–3 taps only.
- **Roster accuracy:** CSV for now, SMS check-in later.
- **PHI:** first name only, 24h TTL, HTTPS.

---

### Open questions

- Is “Start” SMS needed? (MVP: no).
- Add room link in v1? (no).
- Add “Late Add” backdating? (no).
