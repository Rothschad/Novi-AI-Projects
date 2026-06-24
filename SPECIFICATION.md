# SPECIFICATION.md — Public Good (Madrid Greenery Initiative)

Detailed behaviour for each part: what it does, the data it handles, error
handling, examples, and edge cases. Pairs with ARCHITECTURE.md.

---

## A. Public web app

### A1. Question screen — `/q/:questionId`
**Does:** Shows one question + benefit explanation + Yes/No. The entry point a
QR code points to.

**Data in:** `questionId` (from URL).
**Data out:** a vote (`POST /votes`).

**Render:**
```
┌──────────────────────────────────────────┐
│  SALAMANCA                                │
│                                           │
│  Would you like more greenery in your     │
│  area — trees, grass, flowers, bushes?    │
│                                           │
│  Why it matters: greenery lowers local    │
│  temperature 2–4°C, cleans the air, and   │
│  supports wellbeing.                      │
│                                           │
│  198 people agree so far · goal 200       │
│  [██████████████████░░] 99%               │
│                                           │
│  [   YES   ]        [   NO   ]            │
└──────────────────────────────────────────┘
```

**Rules:**
- If `status != active` or past `deadline` → show **Result** screen instead.
- If this device already voted → show **Result** with "You've already voted."
- Progress shows `yes_count` vs `yes_threshold` only (No votes hidden publicly).

**Errors:**
| Condition | HTTP | UX |
|---|---|---|
| Unknown id | 404 | "This question doesn't exist or was removed." |
| Closed/expired | 410 | Show final result + council contact |
| Network fail | — | Inline retry button, keep choice |

**Edge cases:**
- Double-tap submit → button disables on first tap; idempotent by `(voter_hash, id)`.
- Threshold crossed by *this* vote → response includes `just_reached: true` so the
  Thank-you screen congratulates and triggers the notification opt-in.

---

### A2. Thank-you screen
**Does:** Confirms the vote and drives sharing. Optionally collects private feedback.

**Render:** "✓ Thank you for voting." → **Share with a friend** (copy link,
WhatsApp, SMS) → optional one-line feedback box ("Anything else? (private)") →
"See the result".

**Share link:** `https://app/q/:questionId` (same QR target, so shares reuse it).

**Data out:** optional `POST /feedback`.

**Edge case:** feedback empty → skip silently. Feedback never shown to public.

---

### A3. Result screen — `/q/:questionId/result`
**Does:** Shows progress or final outcome + the responsible council's contact.

**States:**
- **Active:** "198 / 200 — almost there. Closes 15 Jul."
- **Passed:** "🎉 200+ neighbours agreed. This is being sent to Salamanca council." +
  `CouncilContactCard` + (Phase 2) GoFundMe button if `gofundme_url` set.
- **Failed/closed:** "This didn't reach its goal by the deadline."

**Data in:** question (counts, status, deadline) + district (council contacts).

---

## B. Backend API

Base: `/api`. JSON in/out. All writes validated and rate-limited.

### B1. `GET /questions/:id`
Returns one question (+ derived `threshold_met`, `closed`). 404 if missing.
```json
{ "question_id":"q-001-salamanca","district_id":1,
  "text":"…","benefit_explanation":"…",
  "yes_count":198,"yes_threshold":200,"deadline":"2026-07-15T23:59:59Z",
  "status":"active","threshold_met":false }
```

### B2. `POST /votes`
**Body:** `{ "question_id":"q-001-salamanca", "choice":"yes" }`
(`voter_hash` derived server-side from IP + UA — never trust client.)

**Success 201:**
```json
{ "ok":true, "yes_count":199, "no_count":47,
  "threshold_met":false, "just_reached":false }
```
**Logic:**
1. Load question → if missing 404, if closed/expired 410.
2. Compute `voter_hash`; if `(voter_hash,id)` exists → 409 `ALREADY_VOTED`.
3. Insert vote; increment denormalised count.
4. If `choice=="yes"` and `yes_count >= yes_threshold` and `!notified`:
   set `status=passed`, `notified=true`, enqueue notification, return `just_reached:true`.

**Errors:** 400 invalid `choice`; 404 unknown; 410 closed; 409 duplicate; 429 rate-limited; 500.

### B3. `GET /districts` / `GET /districts/:id`
Returns scraped district data (population, council leaders, budget, roadmap,
greenery/temp/air metrics). Public may read council contact; admin reads all.

### B4. `GET /districts/:id/questions`
All questions for a district with live counts.

### B5. `POST /feedback`
`{ "question_id":"…","text":"…" }` → 201. Stored private. Rate-limited. Max 1000 chars.

### B6. Notification trigger (internal)
On `just_reached`: create `notifications` row, send Web Push to opted-in devices
for that question + email the admin. Idempotent via `notified` flag.

---

## C. Admin dashboard

### C1. Overview
Table of 21 districts: population, budget, # active questions, total yes votes,
# passed. Sortable by "need" score (low greenery + high temp + poor air).

### C2. Question manager
Create/edit/close a question; set `text`, `benefit_explanation`, `yes_threshold`,
`deadline`. **Generate QR** → PNG/SVG of `qr_target_url` for printing.
Edge: closing a question freezes counts and flips Result screen to final state.

### C3. Feedback & export
Searchable private feedback per question. Export votes + feedback + district data
as CSV/JSON for analysis (the creator's data goal).

---

## D. Madrid data scraper

**Does:** Seeds and refreshes the 21 `districts` from datos.madrid.es.
**Captures:** name, population, council leaders + contacts, annual budget,
roadmap URL, and (where available) greenery %, summer temp, air-quality index.

**Run:** one-off seed before launch; weekly cron refresh (`last_scraped` stamps).

**Error handling:** missing field → keep prior value, flag `data_gaps[]`, never
block a district from having questions. Source unreachable → log + retry, keep
last good snapshot.

**Edge cases:** multiple council leaders → store all, mark primary; renamed/merged
districts → map to the 21 canonical IDs.

---

## E. Phase 2 (specified, not built Week 1)

### E1. GoFundMe
After `status=passed`, admin attaches an external `gofundme_url`. Result screen
shows a "Chip in" button. **App holds no money;** GoFundMe handles pledges and
refunds-if-unmet. Spec assumption — confirm before building.

### E2. Council conversation → public "PR story"
After threshold, admin contacts the council (using scraped contacts) off-platform,
then publishes the council's response as a public, read-only **update** on the
Result screen (timeline of "what happened next"). Voters can read; not chat.

---

## F. Cross-cutting

**Validation:** whitelist `choice ∈ {yes,no}`; sanitise/escape all text; cap
feedback length; reject unknown ids early.

**Rate limits:** votes 1/min/IP; feedback 5/hour/IP; admin exempt.

**Privacy:** `voter_hash` is salted SHA-256 of IP+UA, stored for dedupe only;
no names, emails, or precise location from voters.

**Analytics the creator gets:** per-district yes/no totals + rate, time-to-threshold,
share-driven traffic, private feedback themes, and which districts mobilise fastest.
