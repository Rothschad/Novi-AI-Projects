# DESIGN.md — Public Good (Madrid Greenery Initiative)

**This is the front-end / UI / design brief for Lovable.** It defines the visual
system, components, and every screen + state. Behaviour and data come from
**ARCHITECTURE.md** and **SPECIFICATION.md** — build the UI to match those.

> Build a **responsive web app** (mobile-first, also great on desktop). No native
> app. A resident scans a QR code on a neighbourhood sign and lands directly on a
> single **Question screen**. The whole public experience is 3 screens:
> **Question → Thank-you → Result.** It must feel fast, friendly, trustworthy, and
> take under 10 seconds to vote.

---

## 1. Design principles
1. **One thing per screen.** Never make the voter scroll to find the action. The
   Yes/No choice is always visible without scrolling on a phone.
2. **Calm, natural, optimistic.** This is about greening the city — fresh, light,
   hopeful. Not corporate, not "government grey," not alarmist.
3. **Trust through clarity.** Plain language, visible privacy reassurance, no
   sign-up, no dark patterns.
4. **Big tap targets, big type.** Designed for someone standing on a street with
   one thumb and sunlight on their screen.
5. **Delight at the moment of impact.** The vote and the "it passed!" moment get
   a small, joyful animation. Everywhere else stays quiet.

---

## 2. Visual identity

### 2.1 Colour palette
Use these as design tokens (CSS variables / theme).

| Token | Hex | Use |
|---|---|---|
| `--green-900 / ink` | `#16271E` | Primary text, headings |
| `--green-700 / forest` | `#1F7A4D` | Brand, eyebrow labels, links |
| `--green-500 / leaf` | `#2FB46C` | **Primary CTA (Yes)**, progress fill |
| `--green-300 / sprout`| `#7FD8A4` | Hover tints, highlights |
| `--mint-100 / surface`| `#E9F6EE` | Card tint, chips, section backgrounds |
| `--paper / bg` | `#FBFBF6` | App background (warm off-white) |
| `--muted` | `#5C6B63` | Secondary text, captions |
| `--line` | `#E2E6E1` | Borders, dividers |
| `--amber-400 / sun` | `#F4B740` | "Almost there", accents, sun motif |
| `--sky-400 / air` | `#4FA8C9` | Info accents (air-quality icon) |
| `--terracotta / error`| `#C0492F` | Errors only (never for "No") |

**Important:** "No" is a legitimate answer, **not** a negative — never colour it
red. Style it as a neutral outline button.

Backgrounds: public screens sit on `--paper`, optionally with a very subtle
top-to-bottom mint gradient (`--mint-100` → `--paper`) and a faint leaf/foliage
illustration in a corner at low opacity. Keep it light, never busy.

### 2.2 Typography
- **Primary family:** `Plus Jakarta Sans` (Google Font) for everything.
- **Optional display accent:** `Fraunces` (soft serif) for the big question text
  only — gives a warm, human, "manifesto" feel. If using one font, use Plus
  Jakarta Sans throughout.
- Weights: 400 (body), 500 (labels), 600 (buttons/subheads), 700 (headlines).

**Type scale (mobile → desktop):**
| Role | Size | Weight |
|---|---|---|
| Question (display) | 26 → 34px | 700 (or Fraunces 600) |
| H1 / screen title | 22 → 28px | 700 |
| H2 / section | 18 → 20px | 600 |
| Body | 16 → 17px | 400 |
| Button label | 17px | 600 |
| Caption / privacy | 13px | 500 |

Line-height 1.3 for headings, 1.5 for body. Never below 13px.

### 2.3 Shape, spacing, elevation
- **Spacing scale:** 4 · 8 · 12 · 16 · 24 · 32 · 48 · 64 (4px base).
- **Radius:** cards `20px`, inputs/secondary buttons `14px`, **primary CTA `999px`
  (pill)**, chips `999px`.
- **Shadow:** one soft token — `0 8px 24px rgba(22,39,30,0.08)`. Cards float gently
  on the background; avoid heavy borders.
- **Container:** public content in a centred card, **max-width 460px**, generous
  padding (24px mobile, 32px desktop).

### 2.4 Iconography & imagery
- Line icons, rounded, ~2px stroke (Lucide / Phosphor style).
- Benefit icons: 🌡️ thermometer (cooler), 💨 wind (cleaner air), 💚 heart
  (wellbeing) — render as line icons, not emoji, tinted with the relevant accent.
- Motifs: simple leaf, tree, sprout. Use sparingly as decoration, low opacity.
- No stock photos of stern officials. If any imagery, use soft illustrated
  greenery.

---

## 3. Component library
Build these reusable components (names match ARCHITECTURE §2.1).

- **`DistrictBadge`** — pill, `--mint-100` bg, `--forest` text, small location/leaf
  icon. e.g. "SALAMANCA".
- **`QuestionCard`** — the hero container holding badge, question, benefit, progress,
  votes. The card *is* the screen on mobile.
- **`BenefitExplainer`** — "Why it matters" block; three icon+label rows or a single
  friendly sentence with inline icons.
- **`VoteButtons`** — `Yes` = full-width pill, `--leaf` bg, white text, leaf/check
  icon. `No` = full-width or half, outline (`--line` border, ink text). Stack on
  mobile, side-by-side on wider screens. Min height 56px.
- **`ProgressBar`** — rounded track (`--line`), fill `--leaf`; when ≥90% of goal,
  fill shifts to `--amber` and label reads "Almost there!". Shows `yes_count` vs
  `yes_threshold` only (never expose No counts publicly).
- **`ShareSheet`** — row of buttons: Copy link, WhatsApp, SMS. Big, friendly,
  icon+label. Copy shows a "Copied!" toast.
- **`FeedbackBox`** — single-line/short textarea, placeholder "Anything else?
  (private)", helper text "Only the organisers see this." Submit is secondary.
- **`ResultPanel`** — adapts to state (active / passed / failed) — see §4.3.
- **`CouncilContactCard`** — read-only card: council name, responsible leader,
  email/phone, link to roadmap. Calm, informative.
- **`Toast`** — small, bottom-centre, auto-dismiss (Copied!, Vote counted, errors).
- Admin: **`StatCard`**, **`DataTable`** (sortable), **`QRCard`** (preview +
  download PNG/SVG), **`FeedbackList`**.

**Button states for all buttons:** default · hover (slight darken + lift) · active
(scale 0.97) · focus (2px `--forest` ring, never remove outline) · disabled
(reduced opacity, no shadow) · loading (spinner, label "…").

---

## 4. Screens & states (public app)

### 4.1 Question screen — `/q/:questionId`
The QR landing page. Everything fits one mobile viewport, no scroll to vote.

```
┌───────────────────────────────────┐
│            🌳 Public Good          │  ← tiny wordmark, top
│                                   │
│   ┌───────────────────────────┐   │
│   │  ● SALAMANCA              │   │  ← DistrictBadge
│   │                           │   │
│   │  Would you like more      │   │  ← Question (display type)
│   │  greenery in your area —  │   │
│   │  trees, grass, flowers,   │   │
│   │  bushes?                  │   │
│   │                           │   │
│   │  Why it matters           │   │  ← BenefitExplainer
│   │  🌡 Cooler  💨 Cleaner air │   │
│   │  💚 Better wellbeing       │   │
│   │                           │   │
│   │  198 neighbours agree     │   │  ← progress label
│   │  ▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▱  goal 200 │   │  ← ProgressBar
│   │                           │   │
│   │  ┌───────────────────────┐│   │
│   │  │        YES  🌱         ││   │  ← primary pill
│   │  └───────────────────────┘│   │
│   │  ┌───────────────────────┐│   │
│   │  │         No            ││   │  ← outline
│   │  └───────────────────────┘│   │
│   └───────────────────────────┘   │
│   Anonymous · one vote · no signup │  ← privacy caption
└───────────────────────────────────┘
```

**States:**
- **Loading:** skeleton of the card (shimmer blocks for badge, question, buttons).
- **Submitting:** tapped button shows spinner; both buttons disabled.
- **Already voted:** route to Result with a calm banner "You've already voted —
  here's how it's going."
- **Closed/expired (`status≠active` or past deadline):** show Result instead.
- **Network error:** inline message + "Try again" button; keep the user's choice.
- **Unknown id (404):** friendly NotFound (see 4.4).

### 4.2 Thank-you screen
Triggered right after a successful vote. The feel-good beat.

```
        ✓  (animated check draw)
     Thank you for voting!
   You're helping green Salamanca.

   Share with a neighbour
   [ Copy link ]  [ WhatsApp ]  [ SMS ]

   Anything else? (private)
   [____________________________]  [Send]

         → See the result
```
- The checkmark animates once (draw-in). If **this vote crossed the threshold**
  (`just_reached`), show a small confetti burst and the line "🎉 You pushed it over
  the line!" plus a notification opt-in ("Get told when the council responds").
- Feedback box optional; empty = skip silently. Show "Thanks!" toast on send.

### 4.3 Result screen — `/q/:questionId/result`
One component, three states.

- **Active:**
  ```
  198 / 200  ·  almost there
  ▰▰▰▰▰▰▰▰▰▰▰▰▰▰▰▱
  Closes 15 Jul · 6 days left
  [ Share to push it over ]
  ```
- **Passed (celebration):** confetti on load (respect reduced-motion), big green
  check, "🎉 200+ neighbours agreed. This is being sent to Salamanca council." +
  **`CouncilContactCard`**. Reserve space for a Phase-2 "Chip in" (GoFundMe) button
  and a "What happened next" timeline — **hidden unless data exists.**
- **Failed / closed:** quiet, kind. "This didn't reach its goal this time." Show
  final tally + council contact + "Start one for your street" (future).

### 4.4 NotFound / Closed
Friendly empty state: leaf illustration, "This question isn't available," and a
link to learn what Public Good is. Never a stack trace.

---

## 5. Admin dashboard (functional, not flashy)
Same tokens, denser layout. Desktop-first, has a left sidebar (Overview ·
Questions · Feedback · Export). Voter screens are the star; admin is utilitarian
but clean.

- **Login:** minimal centred card, email/password (or magic link). Brand mark.
- **Overview:** row of `StatCard`s (total votes, questions passed, active, avg
  time-to-threshold) above a sortable **`DataTable`** of the 21 districts
  (population, budget, # active questions, total yes, # passed, **need score**).
  Colour the need score with a subtle green→amber scale.
- **District detail:** district data side-by-side with its questions + live counts.
- **Question manager:** form (text, benefit, threshold, deadline) + **`QRCard`**
  that previews and downloads the QR (PNG/SVG) for printing. Close-question action
  with confirm.
- **Feedback:** searchable private list per question. Clearly labelled "Private —
  never shown publicly."
- **Export:** buttons for CSV / JSON (votes + feedback + district data).

---

## 6. Motion
- **Durations:** 150ms (taps/hovers), 300ms (screen transitions, progress fill),
  600ms (celebration). Easing: `cubic-bezier(0.22, 1, 0.36, 1)` (gentle ease-out).
- Button press: scale to 0.97. Progress bar: animate fill on load. Thank-you:
  checkmark draw. Passed: one confetti burst.
- **Respect `prefers-reduced-motion`:** disable confetti and non-essential
  animation; keep instant state changes.

---

## 7. Accessibility (required)
- WCAG **AA** contrast for all text and the primary button.
- Tap targets **≥ 44×44px**; primary CTA ≥ 56px tall.
- Never rely on colour alone — Yes/No always carry text labels (and an icon).
- Visible focus rings (2px `--forest`); full keyboard operability.
- Proper labels/roles: buttons are `<button>`, progress uses `role="progressbar"`
  with aria values, toasts use `aria-live="polite"`.
- Works one-handed; readable in bright sunlight (high contrast, large type).

---

## 8. Responsive behaviour
- **Mobile (default):** single centred `QuestionCard`, full-width stacked buttons,
  content fits one viewport.
- **Tablet/desktop:** same card centred on the mint-gradient background with the
  foliage motif; Yes/No may sit side-by-side; max-width stays ~460px so it never
  feels stretched. Admin expands to a full sidebar layout.

---

## 9. What to hand Lovable
Build the **public app first** (Question → Thank-you → Result) to a polished,
animated, accessible standard using the tokens above — that's the surface 5,000
people will touch. Then the **admin dashboard** using the same design system.
Wire everything to the endpoints in SPECIFICATION.md (§B). Greenery question text
and benefit copy come from each `question` record; never hard-code a single
district.
