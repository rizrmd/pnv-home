---
date: 2026-05-27
channel: website
topic: landing-page-v1-design-handoff
format: handoff
status: draft
performance:
notes: Design handoff doc for landing-page-v1.html
---

# pnv Landing Page v1 — Design Handoff

> **File:** `content/website/_published/2026-05-27_landing-page-v1.html`
> **URL:** https://pnv.one
> **Status:** Published v1 — ready for design review and iteration

---

## 1. Design Direction

**Aesthetic:** Watch Dogs ctOS / terminal UI. Dark, technical, engineer-native. Feels like a tool, not a marketing site.

**Persona:** Developer, QA engineer, ops engineer. Skeptical of marketing. Responds to specifics, not promises.

**Positioning:** Against two alternatives — code-based automation (Playwright/Selenium) and AI agents (Browser Use/Browserbase). Both must be visually and verbally addressed.

---

## 2. Design Tokens

### Colors

| Token | Value | Usage |
|-------|-------|-------|
| `--bg` | `#07070f` | Page background |
| `--bg-2` | `#0c0c1a` | Cards, panels |
| `--bg-card` | `#101020` | Feature cards |
| `--blue` | `#4ecde6` | Primary accent, CTA, highlights |
| `--blue-bright` | `#00e5ff` | Hover state |
| `--blue-dim` | `rgba(78,205,230,0.08)` | Badge backgrounds |
| `--blue-border` | `rgba(78,205,230,0.22)` | Borders |
| `--blue-glow` | `rgba(78,205,230,0.35)` | Box shadows, glow effects |
| `--white` | `#eef2f7` | Body text |
| `--white-70` | `rgba(238,242,247,0.65)` | Secondary text |
| `--white-30` | `rgba(238,242,247,0.28)` | Tertiary/muted text |
| `--border` | `rgba(238,242,247,0.07)` | Dividers |
| `--red` | `#ef4444` | Error states, problem icons |
| `--green` | `#22c55e` | Success states |

### Typography

| Role | Font | Size | Weight |
|------|------|------|--------|
| Body | Space Grotesk | 16px / 1.6 | 400 |
| H1 (hero) | Space Grotesk | clamp(38px, 6.5vw, 84px) | 700 |
| H2 (sections) | Space Grotesk | clamp(26px, 3.8vw, 48px) | 700 |
| H3 (cards) | Space Grotesk | 15–17px | 600 |
| Monospace labels | JetBrains Mono | 10–13px | 400–700 |
| CTA buttons | Space Grotesk | 14–15px | 600 |

Letter-spacing on headings: `-0.03em` to `-0.04em` (tight).  
Section labels: `0.18em` uppercase monospace.

---

## 3. Components

### Button
Two variants. Both use `clip-path: polygon(10px 0%, ...)` — parallelogram shape.

- **Primary** `.btn-primary`: blue fill `#4ecde6`, dark text, hover: `#00e5ff` + glow shadow
- **Ghost** `.btn-ghost`: transparent, blue border, hover: blue text

### Section Label
`MONOSPACE · UPPERCASE · BLUE` with a 28px line before the text.

### Terminal / Transcript Mockup (Hero)
The hero visual. Simulates the pnv interaction transcript UI:
- Window bar with red/amber/green dots
- Table: `#` / ACTION / DETAIL / STATUS columns
- Selected rows highlighted with blue left-border + blue dim background
- Footer bar: "X STEPS SELECTED · Y VARIABLES DETECTED" + "CONVERT TO TASK" button
- Corner accent brackets (`.corner-tl`, `.corner-tr`, `.corner-bl`, `.corner-br`)

### Data Panel (Solution section)
Simulates a task status readout. Key-value pairs in monospace. Values colored by semantic state (blue = deterministic, red = false, green = success). Progress bar for success rate.

### Prob/Feat/Trust/Pricing Grid
1px-gap grid using `background: var(--border)` as gutter. Cards as solid panels on top. Common pattern: 3-column (desktop), 1-column (mobile).

### FAQ Accordion
Expand/collapse with JS. Icon toggles `+` / `-`. Open state gets blue filled icon.

### Glitch Effect (H1)
CSS `::before` / `::after` pseudo-elements with `clip-path` split and offset animation. Fires every 6s, subtle.

### Scanlines
Full-page fixed overlay via `body::after`. Very subtle (`rgba(0,0,0,0.025)`). Reinforces terminal aesthetic.

### Grid Background
`.grid-bg` — absolute inset, 48×48px grid in blue at 3.5% opacity. Used in Hero and CTA sections.

---

## 4. Page Structure

| Section | ID / Class | Content |
|---------|-----------|---------|
| Nav | `nav` | Logo · "SYSTEM ONLINE" pulse · Feature links · CTA button |
| Hero | `.hero` | Badge · H1 with glitch · Subhead · CTA buttons · Terminal mockup · Note |
| Problem | *(no id)* | 3 cards: Writing code / Prompting AI / The shared flaw |
| Solution | *(no id)* | Split: text left / data panel right |
| Features | `#features` | 5 cards (first is 2-col wide): Profiles · Transcript · Deterministic replay · Task creation · Scheduling |
| Social Proof | *(no id)* | 3 trust metrics (100%, 0, ∞) · Quote block |
| How it works | `#how-it-works` | 4 numbered steps with connecting line |
| Pricing | `#pricing` | 3 tiers: Free / Pro ($10) / Team ($15) |
| FAQ | `#faq` | 5 questions |
| CTA | `.cta-wrap` | Closing hero block with grid + glow |
| Footer | `footer` | Brand name · "Built by Rizky from Indonesia" · Links |

---

## 5. Copy — Key Lines

**Hero H1:**
> Automate the browser.
> No code. No AI.
> No surprises.

**Hero sub:**
> pnv records everything you do in a cloud browser, lets you pick the steps you want to repeat, and replays them exactly — every time.

**Hero note:**
> No credit card · No code · 2 minutes to your first task

**Problem H2:**
> Browser automation is broken for everyone except engineers.

**Solution H2:**
> Do it once. pnv turns the doing into the automation.

**Features H2:**
> Everything you need to automate the browser. Nothing you don't.

**Social proof metrics:**
- `100%` — Deterministic execution. No LLM, no interpretation, no variance between runs.
- `0` — Lines of code required. Interact normally. pnv handles the rest.
- `∞` — Executions from one recorded task. Different inputs each time, same reliable result.

**CTA H2:**
> Your next automation is one interaction away.

**CTAs:** "Get started free" (primary) · "See how it works" (ghost) · "View on GitHub" (ghost)

---

## 6. Interactions & Animations

| Element | Animation | Details |
|---------|-----------|---------|
| Glitch text | CSS keyframes, 6s loop | Fires briefly at 88–96% of cycle |
| Pulse dot | `blink`, 1.8s ease-in-out | Nav status + hero badge |
| Progress bar | `fillup`, 1.8s ease-out | Solution section success rate |
| FAQ accordion | CSS `max-height` transition | 0.35s ease |
| Button hover | `translateY(-1px)` + glow | Primary button only |
| Feature card hover | Background lightens + icon glow | 0.25s |
| Scroll | `scroll-behavior: smooth` | Anchor links |

---

## 7. Responsive Breakpoints

**Breakpoint:** `max-width: 960px`

| Element | Desktop | Mobile |
|---------|---------|--------|
| Nav links | Visible | Hidden |
| "SYSTEM ONLINE" status | Visible | Hidden |
| Hero padding | 120/48/80px | 100/24/60px |
| Section padding | 96/48px | 64/24px |
| Problem / Feature / Pricing / Trust grids | 3-col | 1-col |
| Solution grid | 2-col | 1-col, 40px gap |
| How it works steps | 4-col | 2-col, no connector line |
| Wide feature card | spans 2 cols | 1-col |
| Footer | flex row | flex col, centered |
| CTA buttons | flex row | flex col, centered |

---

## 8. Open Items / Design Notes

- **Logo:** `img src="Logo_1.png"` with `filter: invert(1) brightness(2)`. File not in this folder — needs to be placed at the same path as the HTML, or path updated to match actual asset location.
- **Quote attribution:** Currently `"— ENGINEERING LEAD // EARLY ACCESS TESTER"` — placeholder. Replace with real name/company when available.
- **Social proof metrics (100%, 0, ∞):** Product-truth metrics, not user metrics. Still pre-launch, no real user numbers. Revisit when launch data exists.
- **No mobile nav menu:** Nav links and status are hidden on mobile with no hamburger menu. Consider adding a mobile nav if link clicks matter.
- **No animations on scroll:** All animations are CSS-only, not scroll-triggered. Hero animations fire on page load regardless of scroll position. Consider IntersectionObserver for progress bar + step animations.
- **GitHub link:** `https://github.com/pnv-one` in footer and CTA. Confirm repo is public before launch.

---

## 9. Assets Referenced

| Asset | Path in HTML | Status |
|-------|-------------|--------|
| Logo | `Logo_1.png` | Placeholder — file must be co-located or path updated |
| Space Grotesk | Google Fonts CDN | External dependency |
| JetBrains Mono | Google Fonts CDN | External dependency |
| Icons | Inline SVG | Self-contained |
