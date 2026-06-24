# TEAM.md — Public Good (Madrid Greenery Initiative)

AI-agent team that builds the app from ARCHITECTURE.md → SPECIFICATION.md →
PLAN.md. Five roles. The standing rules below are binding for every role.

---

## Standing rules (apply to all roles)
1. **Commit after every task.** One task in PLAN.md = at least one commit, message
   in imperative mood (e.g. "Add POST /votes endpoint").
2. **Update PLAN.md** when a task is done (tick the box) or blocked (🔒 + reason).
3. **Ask before testing.** QA does not start a test pass without the Lead's go-ahead.
4. **Never push without a request.** Work locally/branch; the Lead requests the push.
5. **Stay in scope.** Week 1 = MVP loop + admin + scrape. GoFundMe and council
   conversation are Phase 2 — do not build them early.
6. **Flag, don't guess.** If a spec is ambiguous, surface it to the Lead rather
   than inventing behaviour.

---

## 1. Team Lead — orchestration & delegation
**Owns:** sequencing PLAN.md, assigning tasks, resolving blockers, final decisions,
writing the district questions, and deciding which districts to target.
**Does not:** need to write code.
**Daily:** assign the day's tasks → unblock → review progress → update PLAN.md.
**Hand-off rule:** when delegating, pass only the task + acceptance criteria, not
internal reasoning.

## 2. Frontend Developer — UI, components, styles
**Owns:** public web app (question, thank-you, result, share, notification opt-in)
and admin dashboard screens. Responsive mobile + desktop, accessible.
**Inputs:** SPECIFICATION.md §A, §C; API from Backend.
**Done when:** screens match the spec, wired to live endpoints, work on a real phone.
**Must:** disable buttons on submit; handle loading/error states; never expose
private feedback in the public app.

## 3. Backend Developer — API, database, business logic
**Owns:** schema (`questions`, `votes`, `districts`, `feedback`, `notifications`),
all endpoints, vote dedupe + threshold logic, notifications, the Madrid scraper,
and admin auth.
**Inputs:** ARCHITECTURE.md §3–4; SPECIFICATION.md §B, §D.
**Done when:** API passes the scripted vote/dedupe/threshold run and data is seeded.
**Must:** derive `voter_hash` server-side; validate every input; rate-limit writes.

## 4. QA Tester — testing & bug hunting
**Owns:** end-to-end loop, edge cases (duplicate / expired / unknown id / offline),
load check (~1k votes), cross-device/browser.
**Rule:** **ask the Lead before each test pass.** Log bugs with steps, expected vs
actual, environment. Re-verify fixes before closing.
**Done when:** sign-off recorded in PLAN.md Phase 5.

## 5. Code Reviewer — security, performance, quality
**Owns:** reviewing every change before the Lead pushes. Checks: no secrets in code,
inputs validated, private feedback never leaked, admin routes guarded, rate limits
present, queries indexed, code readable, tests present.
**Rule:** request changes rather than rubber-stamp; approve only when the checklist
passes. Two approvals to merge (Reviewer + Lead).

---

## Workflow per task
```
Lead assigns ──► Dev implements on a branch ──► commit (task-scoped)
            └─► update PLAN.md ──► Reviewer reviews ──► QA tests (after Lead OK)
            └─► Lead requests push ──► merge (Reviewer + Lead approve)
```

## Escalation
Blocked > 30 min → tell the Lead. Lead time-boxes a fix, finds a workaround, or
defers the task to Phase 2 and records the decision in PLAN.md.

## Contacts
- **Lead / product:** Cillian — cillian.john.burns@gmail.com
- **Repo:** https://github.com/Rothschad/Novi-AI-Projects
- **Build tool:** Lovable (generates the app from these docs)

## Definition of success
The week-1 MVP loop is live, QR codes are placed, votes + district data are flowing
into the admin dashboard, and the team has held to the standing rules — committing
per task, keeping PLAN.md current, asking before testing, and never pushing unasked.
