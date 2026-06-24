# ARCHITECTURE.md — Public Good (Madrid Greenery Initiative)

> Civic-action app: residents scan a QR code in their neighbourhood, answer one
> yes/no question about local greenery, and — if enough people agree by a
> deadline — the idea is pushed to the district council. The creator collects
> district-level data to decide where to target.

**Stack owner:** Lovable generates the app. This document describes *what* to
build so Lovable (and the agent team) produce the right thing.

**Platforms:** Mobile web + desktop web (responsive, single codebase).
**Timeline:** 1 week. **Budget:** €0 (free tiers only). **Initial users:** ~5,000.

---

## 1. Scope (what ships when)

| Capability | Phase | Notes |
|---|---|---|
| QR → question → yes/no vote | **Week 1 (MVP)** | Core loop |
| Benefit explanation on question | **Week 1** | Static text per question |
| "Thank you" + share link | **Week 1** | Viral growth |
| Threshold + deadline logic | **Week 1** | Per-question target |
| "Your issue is being heard" notification | **Week 1** | Fired at threshold |
| Admin data dashboard (votes + district data) | **Week 1** | Creator's data goal |
| Madrid district data scrape (21 districts) | **Week 1** | Population, council, budget, roadmap |
| GoFundMe (unlock post-threshold, refund if unmet) | **Phase 2** | External, assumption — confirm |
| Council-member conversation → public "PR story" | **Phase 2** | Admin-mediated, assumption — confirm |

---

## 2. System parts

```
                         ┌──────────────────────────┐
   Physical QR code  ──► │  PUBLIC WEB APP (voter)   │
   (printed, placed)     │  /q/:questionId          │
                         │  - Question + benefits    │
                         │  - Yes / No               │
                         │  - Thank-you + Share      │
                         │  - Progress + result      │
                         └────────────┬─────────────┘
                                      │ REST/JSON
                         ┌────────────▼─────────────┐
                         │       BACKEND API         │
                         │  votes · questions ·      │
                         │  districts · notify       │
                         └────────────┬─────────────┘
                                      │
                ┌─────────────────────┼─────────────────────┐
                │                     │                     │
       ┌────────▼───────┐   ┌─────────▼────────┐   ┌────────▼────────┐
       │   DATABASE      │   │  NOTIFICATIONS    │   │  ADMIN DASHBOARD │
       │ questions/votes │   │  push at threshold│   │  (creator only)  │
       │ districts       │   └──────────────────┘   │  votes + data    │
       └─────────────────┘                          └─────────┬────────┘
                ▲                                              │
                │ seed (one-off + weekly refresh)              │
       ┌────────┴───────────────────────────────────┐         │
       │  MADRID DATA SCRAPER (datos.madrid.es)      │◄────────┘
       │  21 districts: population, council leaders, │
       │  budget, roadmap, public structures         │
       └─────────────────────────────────────────────┘
```

### 2.1 Public web app (voter-facing)
- **Pages:** `Question` (`/q/:id`), `ThankYou`, `Result`, `NotFound/Closed`.
- **No login.** Anonymous. One vote per question per device/IP.
- **Components:** `QuestionCard`, `BenefitExplainer`, `VoteButtons`, `ShareSheet`,
  `ProgressBar`, `ResultPanel`, `CouncilContactCard` (read-only).

### 2.2 Admin dashboard (creator-facing)
- **Auth required** (single admin / small team).
- **Pages:** `Overview` (all districts), `DistrictDetail`, `QuestionManager`
  (create/edit/close questions + generate QR), `Feedback` (private), `Export`.
- Shows aggregated votes, threshold status, and scraped district data side-by-side.

### 2.3 Backend API
- Thin REST layer over the database. Validates votes, dedupes, counts, and fires
  the notification when a question crosses its threshold.

### 2.4 Database
- Three core collections: `questions`, `votes`, `districts` (+ `feedback`,
  `notifications`). See §3.

### 2.5 Madrid data scraper
- One-off seed + weekly refresh of the 21 districts from
  [datos.madrid.es](https://datos.madrid.es). Feeds `districts` and informs which
  areas to target and what QR questions to create.

---

## 3. Data model

### `districts` (21 rows — Madrid distritos)
```json
{
  "district_id": 1,
  "name": "Salamanca",
  "population": 143800,
  "council_leaders": [
    { "name": "…", "title": "Concejal-Presidente", "email": "…", "phone": "…" }
  ],
  "annual_budget_eur": 2500000,
  "roadmap_url": "https://…",
  "public_data_url": "https://datos.madrid.es/…",
  "greenery_pct": 12,
  "avg_summer_temp_c": 28,
  "air_quality_index": 65,
  "last_scraped": "2026-06-24T10:00:00Z"
}
```

### `questions`
```json
{
  "question_id": "q-001-salamanca",
  "district_id": 1,
  "text": "Would you like more greenery in your area — trees, grass, flowers, bushes?",
  "benefit_explanation": "Greenery lowers local temperature 2–4°C, cleans the air, and supports wellbeing.",
  "qr_target_url": "https://app/q/q-001-salamanca",
  "created_at": "2026-06-24T10:00:00Z",
  "deadline": "2026-07-15T23:59:59Z",
  "yes_threshold": 200,
  "yes_count": 0,
  "no_count": 0,
  "status": "active",            // active | passed | failed | closed
  "notified": false,
  "gofundme_url": null            // Phase 2: set after threshold
}
```

### `votes`
```json
{
  "vote_id": "uuid",
  "question_id": "q-001-salamanca",
  "choice": "yes",               // yes | no
  "voter_hash": "sha256(ip+ua)", // dedupe only, not identifying
  "device": "mobile",
  "created_at": "2026-06-24T14:32:00Z"
}
```

### `feedback` (private — voters cannot read)
```json
{ "feedback_id": "uuid", "question_id": "q-001-salamanca",
  "text": "Our street bakes in summer.", "created_at": "…" }
```

### `notifications`
```json
{ "question_id": "q-001-salamanca", "type": "threshold_reached",
  "sent_at": "…", "recipients": 203 }
```

**Indexes:** `votes(question_id)`, `votes(voter_hash, question_id)` (dedupe),
`questions(district_id)`, `questions(status)`.

---

## 4. External services (all free tier)

| Concern | Choice | Why |
|---|---|---|
| Hosting (web) | Lovable default / Vercel / Firebase Hosting | €0, instant deploy |
| Backend + DB | Supabase or Firebase | €0 tier, realtime, auth built-in |
| Push / notify | Web Push (FCM) + email fallback | €0, no app-store needed |
| QR generation | `qrcode` lib (admin side) | €0, generate per question |
| Data source | datos.madrid.es Open Data | Free, official |
| Donations (Phase 2) | GoFundMe (external link) | Handles money + refunds; we hold no funds |

> **Money:** the app never holds funds. GoFundMe handles escrow/refunds. This
> keeps us out of payment-regulation/KYC scope for Week 1.

---

## 5. Key flows

**Vote loop (MVP):**
`Scan QR → GET /questions/:id → render question + benefits → POST /votes →
increment count → if yes_count ≥ threshold and not notified: fire notification,
set status=passed → ThankYou + Share.`

**Targeting loop (creator):**
`Scrape 21 districts → rank by need (low greenery, high temp, poor air, budget) →
choose target areas → create questions + generate QR → print & place.`

**Dedupe:** `voter_hash = sha256(ip + user-agent)`; unique per `(voter_hash,
question_id)`. Shared networks tolerated via UA component.

---

## 6. Non-functional requirements

- **Privacy:** no accounts, no personal data, IP only as a salted hash; EU data region.
- **Performance:** question load < 500 ms; vote write < 500 ms.
- **Capacity (free tier):** comfortably handles 5k voters × 21 questions.
- **Security:** HTTPS only; input validation; rate-limit votes (1/min/IP);
  admin routes behind auth; private feedback never exposed to public API.
- **Accessibility:** single-question screens, large tap targets, legible contrast.

---

## 7. Open questions (assumptions to confirm)
1. GoFundMe = external link, post-threshold, refunds via GoFundMe? (assumed yes)
2. Council conversation = admin-mediated, published as a public update? (assumed yes)
3. QR codes placed by you manually, one question per area? (assumed yes)
4. One active greenery question per district at launch? (assumed yes)
