# PLAN.md — Public Good (Madrid Greenery Initiative)

One-week build. Phases are sequential; tasks within a phase list their owner,
dependencies, and the concrete result that proves the task is done. **Update this
file as you go** — tick boxes, add an `UPDATE:` note when scope or timing changes.

Legend: ☐ todo · ☑ done · 🔒 blocked. Owners map to TEAM.md roles.

---

## Phase 0 — Project setup (Day 1, ½ day)
**Result:** repo, Lovable project, and Firebase/Supabase backend exist and connect.

- ☐ **0.1** Confirm backend choice (Supabase or Firebase) — *Lead* — no deps
- ☐ **0.2** Create Lovable project from ARCHITECTURE.md + SPECIFICATION.md — *FE* — 0.1
- ☐ **0.3** Provision DB + auth (admin), set EU region — *BE* — 0.1
- ☐ **0.4** Wire env vars, deploy empty app to a live URL — *BE* — 0.2,0.3
- **Done when:** the blank app loads at a public HTTPS URL and can reach the DB.

---

## Phase 1 — Data & questions (Day 1–2)
**Result:** 21 districts seeded; one greenery question + QR per target district.

- ☐ **1.1** Scrape 21 districts from datos.madrid.es → `districts` (name, population,
  council leaders, budget, roadmap, greenery/temp/air) — *BE* — 0.3
- ☐ **1.2** Rank districts by "need" (low greenery, high temp, poor air) — *BE/Lead* — 1.1
- ☐ **1.3** Write the greenery question + benefit text per target district — *Lead* — 1.2
- ☐ **1.4** Seed `questions` with thresholds + deadlines — *BE* — 1.3
- ☐ **1.5** Generate a printable QR (PNG/SVG) per question — *BE* — 1.4
- **Done when:** `GET /districts` returns 21; each target district has 1 active
  question; QR images scan to the right `/q/:id`.

---

## Phase 2 — Backend API (Day 2–3)
**Result:** voting works end-to-end through the API with dedupe + threshold logic.

- ☐ **2.1** `GET /questions/:id` (+ derived fields) — *BE* — 1.4
- ☐ **2.2** `POST /votes` (validate, hash, dedupe, count) — *BE* — 2.1
- ☐ **2.3** Threshold detection → set `passed`, `notified`, enqueue notify — *BE* — 2.2
- ☐ **2.4** `GET /districts`, `GET /districts/:id/questions` — *BE* — 1.1
- ☐ **2.5** `POST /feedback` (private, rate-limited) — *BE* — 2.1
- ☐ **2.6** Rate limiting + input validation across writes — *BE* — 2.2
- **Done when:** scripted run can fetch a question, vote, get a duplicate rejected,
  and cross a threshold that flips status to `passed`.

---

## Phase 3 — Public web app (Day 3–4)
**Result:** a person can scan → read → vote → share → see result on phone & desktop.

- ☐ **3.1** Question screen (`/q/:id`) with benefit text + progress — *FE* — 2.1
- ☐ **3.2** Vote buttons wired to `POST /votes`, disabled-on-submit — *FE* — 2.2
- ☐ **3.3** Thank-you screen + Share sheet (copy/WhatsApp/SMS) — *FE* — 3.2
- ☐ **3.4** Optional private feedback box — *FE* — 2.5
- ☐ **3.5** Result screen (active / passed / failed) + council contact — *FE* — 2.4
- ☐ **3.6** Threshold notification opt-in + "issue is being heard" state — *FE* — 2.3
- ☐ **3.7** Responsive pass (mobile + desktop) + a11y — *FE* — 3.1–3.6
- **Done when:** full loop works from a real phone scanning a printed QR.

---

## Phase 4 — Admin dashboard (Day 4–5)
**Result:** creator can see all data and manage questions/QRs.

- ☐ **4.1** Admin auth + route guard — *BE* — 0.3
- ☐ **4.2** Overview table (21 districts, votes, need-score) — *FE* — 2.4
- ☐ **4.3** Question manager (create/edit/close + generate QR) — *FE* — 1.5,2.1
- ☐ **4.4** Private feedback viewer — *FE* — 2.5
- ☐ **4.5** CSV/JSON export (votes + feedback + district data) — *BE* — 2.4
- **Done when:** creator logs in, sees live votes beside district data, exports a file.

---

## Phase 5 — Test, harden, launch (Day 5–6)
**Result:** tested, secure, live, with QR codes ready to place.

- ☐ **5.1** End-to-end test of vote loop across all target districts — *QA* — Phase 3
- ☐ **5.2** Edge cases: duplicate, expired, unknown id, network fail — *QA* — Phase 3
- ☐ **5.3** Load check (~1k votes) on free tier — *QA* — Phase 2
- ☐ **5.4** Security review (rate limit, validation, private feedback, admin auth) — *Reviewer* — Phase 4
- ☐ **5.5** Deploy to production URL; smoke test — *BE* — all
- ☐ **5.6** Print + place QR codes in target districts — *Lead* — 1.5,5.5
- **Done when:** app is live, QA sign-off recorded, QRs are physically out.

---

## Phase 6 — Phase-2 backlog (after launch — NOT week 1)
- ☐ **6.1** GoFundMe: attach external `gofundme_url` post-threshold; show on Result
- ☐ **6.2** Council conversation → published public "PR story" timeline on Result
- ☐ **6.3** Weekly scraper refresh (cron) + data-gap dashboard
- ☐ **6.4** Multi-question per district; new categories beyond greenery

---

## Dependencies (critical path)
`0 → 1 → 2 → 3 → 5 → launch` (Phase 4 can run parallel to 3 once Phase 2 is done).

## Risks / blockers
- Madrid data incomplete → seed with gaps flagged, don't block questions.
- Free-tier limits at ~5k → upgrade later; out of week-1 scope.
- App-store friction → avoided by being web-only (QR opens browser).
- Money/regulation → avoided in week 1 (no in-app funds; GoFundMe is Phase 2).

## Definition of done (week 1)
QR scan → greenery question + benefits → yes/no → thank-you + share → threshold
fires "being heard" notification → admin sees votes beside district data and can
export. GoFundMe + council PR story deferred to Phase 2.
