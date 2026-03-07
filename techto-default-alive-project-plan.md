# TechTO: Default Alive Calculator
### Project Plan for Claude Code

---

## Overview

A modern, mobile-first reimagining of Trevor Blackwell's startup funding calculator (growth.tlb.org), inspired by Paul Graham's essay "Default Alive or Default Dead?" — branded for TechTO and built for Canadian founders.

**Live URL target:** `growth.techto.org`  
**Stack:** React + Tailwind CSS, single-file deployable, no backend required  
**State:** URL-encoded (shareable links, no database)

---

## Inspiration & References

- **Essay:** https://www.paulgraham.com/aord.html
- **Original tool:** https://growth.tlb.org/
- **Original source code:** https://gitlab.com/tlb/startuptools (MIT license — fork to GitHub before starting)
- **TechTO brand:** https://www.techto.org/
- **Visual style:** Light, clean, minimal — matching TechTO homepage aesthetic

---

## GitHub Setup (Do This First)

The original tool is MIT licensed and available on GitLab. Before writing any code:

1. `git clone https://gitlab.com/tlb/startuptools.git`
2. Create a new GitHub repo (e.g. `techto/default-alive-calculator`)
3. Push the cloned repo to GitHub
4. In `README.md`, credit the original: *"Forked from [Trevor Blackwell's startuptools](https://gitlab.com/tlb/startuptools) — MIT License"*
5. Build all new work on top of this fork

Use the original math logic as the foundation. Rewrite the frontend entirely.

---

## Design Direction

### Visual Style — Use Exact TechTO Brand Assets (DO NOT GUESS)
The owner will provide logo files and assets directly. Do not substitute or approximate.

**Colors (exact):**
- `#ebff52` — Electric yellow-green. Primary accent, CTA buttons, highlights
- `#000000` — Black. Primary text, nav, borders
- `#ffffff` — White. Page background, card backgrounds
- `#d2f5ff` — Light blue. Secondary accent, subtle backgrounds

**Background:** White (`#ffffff`) — light, not dark. Match the TechTO homepage.

**Typography (exact font names — load via Google Fonts or uploaded font files):**
- `Feature Display` — Titles, subtitles, headings, quotes. The large serif display font seen in "Canada's Most Connected Tech Community"
- `Artex` — Subheadings, section headers, body text, nav

**Do not substitute Inter, Helvetica, or any other font. Use Feature Display and Artex only.**

**Nav bar:** Match TechTO homepage exactly — white background, black "TECHTO" wordmark (all caps, condensed), clean horizontal nav links, black-outlined CTA button with `#ebff52` hover

**Footer:** Include the geometric lattice/grid pattern from the TechTO homepage footer

**Brand voice:** Punchy, brief, energetic. No fluff. Inspire action.

### Layout — Critical Design Principle
**Get to the chart in under 100px. The chart IS the hero.**

Trevor Blackwell's original tool opens with zero preamble — you land directly on the calculator. This redesign must do the same. No big headline block, no hero section, no eyebrow text, no subtitle paragraph above the fold.

The headline "Are you Default Alive or Default Dead?" belongs only in the browser tab title and optionally as a small subtitle in the nav — NOT as a hero section consuming screen real estate.

**Page order (top to bottom):**
1. Minimal yellow (`#ebff52`) nav bar — TECHTO logo left, links center, "Become a Member" pill right
2. **The chart — immediately, full width. Nothing above it except the nav.**
3. Status pill ("Default Alive ✓" or "Default Dead ✗") directly below chart
4. Weekly / Monthly / Annual toggle
5. Three metric cards: Months to Profit, Capital Needed, Monthly Burn
6. ~~Four input cards~~ — inputs live ON the chart as draggable handles with inline editable labels. No separate form grid.
7. Copy Shareable Link + Export Snapshot buttons
8. "Your Milestones" section
9. Black footer with lattice pattern

---

## Vercel v0 Prompt

Use this prompt verbatim when starting in v0.dev. The goal is to get the visual design right first, then wire up the logic separately.

---

Build a single-page web app called **"Default Alive?"** for TechTO.

**Core design principle: Get to the chart immediately. The chart is the hero. No big headline section above it — just the nav, then the chart. Inspired by Trevor Blackwell's minimalist tool at growth.tlb.org.**

**Brand:**
- Nav bar: `#ebff52` yellow background, black "TECHTO" wordmark (bold, uppercase, tight tracking), nav links (Events, Peerscale, Community, Directory), black-outlined pill CTA "Become a Member" — exactly like techto.org
- Page background: white
- Accent: `#ebff52`
- Fonts: Feature Display (serif, headlines) + Artex (sans, UI). Use Playfair Display and DM Sans as proxies.
- Footer: black background with subtle grid/lattice pattern, white text

**Page layout (top to bottom — in this exact order):**
1. Yellow nav bar as described above. Browser tab title: "Default Alive? — TechTO"
2. **The chart — full width, immediately below the nav, no hero section above it.** Canvas chart showing: green revenue curve, red dashed flat expense line, light blue shaded area between them (capital needed), vertical "PROFITABLE ✓" label marker, and three draggable circle handles on the chart — one on the revenue curve at month 0 (controls revenue), one on the expense line at midpoint (controls expenses), one on the revenue curve slope (controls growth rate). Chart must be fully responsive and never overflow.
3. Status pill — green "Default Alive ✓" or red "Default Dead ✗" with detail text
4. Weekly / Monthly / Annual toggle (pill style)
5. Three metric cards in a row: Months to Profit, Capital Needed, Monthly Burn
6. **Inputs live on the chart — not in a separate form.** Each draggable handle has its current value displayed as an editable number label directly beside it. Click/tap the number to type an exact value, press Enter to confirm. This is the entire input UI. No card grid, no form fields, no mortgage-calculator aesthetic. The handles and their inline labels ARE the controls.
7. Two buttons: "Copy Shareable Link" (filled black) and "Export Snapshot" (outlined)
8. "Your Milestones" section — grid of cards showing time until: $1M ARR, Wealthsimple ($100M ARR), Shopify ($9B ARR), Stripe ($14B ARR), Apple ($391B ARR), plus an "Add custom company +" card
9. Black footer with grid lattice pattern — credits: "Inspired by Trevor Blackwell's calculator and Paul Graham's essay. Built for Canadian founders by TechTO."

**Style:** Clean, minimal, confident. Like YC's website but with TechTO's yellow identity. Generous white space. No decorative elements. The chart and numbers do the talking.

**Functional requirements:**
- All inputs update chart and metrics in real time
- Draggable handles on chart also update the input fields
- URL encodes all state for shareable links
- Fully mobile responsive

---

## Core Features

### 1. Inputs — Sliders First, Exact Entry as Fallback
The draggable handles on the chart ARE the primary UI, exactly like Trevor's original. No separate form below the chart.

Each handle displays its current value as an editable number label directly on or beside it. Click or tap the number to type an exact value, press Enter to confirm. It snaps back to drag mode after confirming.

- Revenue handle → shows and controls current monthly revenue
- Expenses handle → shows and controls current monthly expenses
- Growth handle → shows and controls current monthly growth %
- Cash on hand → a fourth handle or an editable label below the chart

This is not a mortgage calculator. The chart is the interface. Exact number entry is an escape hatch for precision, not the primary interaction. All values update the chart and metrics in real time.

### 2. The Chart
- Smooth curves: Revenue (green) vs. Expenses (red/flat)
- Blue shaded area = capital needed before profitability
- Vertical markers: "Default Alive" / "Default Dead" determination
- Profitability intersection clearly labeled
- **Chart must never clip or overflow — fully responsive at all screen sizes**
- Animated on load / on input change

### 3. Default Alive Status Card
Prominent, above-the-fold verdict:
- ✅ **"You are Default Alive"** — green, with month of profitability
- ❌ **"You are Default Dead"** — red, with how many months of runway remain
- Show: Total capital needed, months to profitability, current burn rate

### 4. Aspirational Comparables (Milestones Panel)
Show how long until the founder reaches major revenue milestones.

**Default companies (hardcoded, aspirational):**
| Company | Annual Revenue |
|---|---|
| Shopify (early) | $1M ARR |
| Wealthsimple | $100M ARR |
| Shopify (today) | $9B ARR |
| Stripe | $14B ARR |
| Apple | $391B ARR |

- Display: "At your current growth rate, you'll pass [Company]'s revenue in [X months / X years]"
- Each milestone shows the company logo (small, greyscale)
- **Search/add custom company:** Founder can type a company name and enter a revenue figure manually
- **Custom logo upload:** Allow founders to upload a logo for their custom comparable
- Milestones highlight as they're crossed (if founder is already past one)

### 5. URL-Encoded State (Shareable Links)
- All input values encoded in URL params on every change
- "Copy Link" button with visual confirmation
- Shareable scenarios: founders can send their exact model to a co-founder or investor
- No login, no database, no backend

### 6. Export / Screenshot Mode
- "Share" button that generates a clean screenshot-optimized view
- Strips inputs, shows only: status card + chart + key metrics
- Designed to look great in a Slack message or email
- Include TechTO logo in exported view

---

## Additional Improvements Over Original Tool

| Issue | Fix |
|---|---|
| Ugly design | Light, modern UI using exact TechTO brand (Feature Display + Artex fonts, #ebff52 accent) |
| Doesn't work on mobile | Mobile-first responsive layout |
| Can't enter exact numbers | Inline editable labels on each handle — click to type exact value, Enter to confirm |
| Chart leaves screen | Fully responsive SVG/canvas chart with proper bounds |
| Hard to share screenshots | Dedicated share/export mode |
| No comparables | Milestones panel with real company benchmarks |
| No branding | TechTO logo, colors, footer |
| No URL sharing | Full URL state encoding |
| No context | Link to PG essay; short explainer text inline |

---

## Copy / Microcopy

### Hero
> **Are you Default Alive or Default Dead?**  
> Enter your numbers. Find out where you really stand.  
> *Inspired by Paul Graham's essay. Built by TechTO.*

### Status Cards
- Default Alive: *"At your current growth rate, you'll reach profitability in [X] months — without raising another dollar."*
- Default Dead: *"At your current burn rate, you'll run out of money in [X] months before hitting profitability. You need a plan."*

### Comparables intro
> *"At your current growth rate, here's when you'll hit the milestones that matter."*

### Footer
> *Inspired by [Trevor Blackwell's calculator](https://growth.tlb.org/) and [Paul Graham's essay](https://www.paulgraham.com/aord.html). Made with ❤️ by [TechTO](https://www.techto.org/) for Canadian founders.*

---

## Tech Stack

- **Framework:** React (single `.jsx` file for easy deployment)
- **Styling:** Tailwind CSS
- **Chart:** Recharts (already available in Claude artifacts environment)
- **State:** React `useState` + `useEffect` for URL encoding/decoding
- **URL encoding:** `URLSearchParams` — no router needed
- **No backend, no auth, no database**

---

## File Structure

```
growth-calculator/
├── index.html          # Shell with React/Tailwind CDN imports
├── App.jsx             # Main component (or single index.html with embedded React)
└── README.md
```

Or as a single `index.html` if deploying to Netlify/Vercel drop.

---

## Development Phases

### Phase 1 — Core Calculator
- Input panel with exact number entry
- Revenue/expense/growth math engine
- Default Alive / Default Dead determination
- Basic chart (Recharts)
- URL state encoding

### Phase 2 — Polish & Mobile
- Responsive layout (mobile-first)
- Chart overflow fix + animation
- Status card design
- TechTO branding + header/footer

### Phase 3 — Comparables
- Hardcoded milestone companies
- Timeline calculation ("X months until you pass Shopify")
- Search/add custom company
- Custom logo upload

### Phase 4 — Share & Export
- "Copy Link" button
- Screenshot/export mode
- Social share formatting

---

## Math Reference (from original tool)

Given:
- `r` = current monthly revenue
- `g` = monthly growth rate (decimal, e.g. 0.1 = 10%)
- `e` = monthly expenses (constant)
- `c` = cash on hand

Revenue in month `n`:  
`R(n) = r * (1 + g)^n`

Profitability month (solve for n where R(n) = e):  
`n = log(e/r) / log(1 + g)`

Cumulative burn before profitability:  
`Σ (e - R(n)) for n = 0 to profitability_month`

Default Alive = `cash on hand > cumulative burn`

---

## Notes for Claude Code / Vercel v0

- **Visual design:** Use Vercel v0 first to nail the UI. Once design is approved, bring to Claude Code to wire up math engine, drag handles, URL state, and milestones logic.
- **Start by cloning the GitLab repo and pushing to GitHub** before writing any new code
- The chart is the first thing users see — it must render correctly on load with sensible defaults
- Use Recharts `AreaChart` or a canvas element for the revenue/expense curves
- Encode URL state with `useEffect` watching all input values
- Test on mobile viewport (375px width) before declaring done
- **Never guess on brand assets** — the owner will provide logo files and font files. Use Playfair Display + DM Sans as proxies until then.
- `Feature Display` is the headline serif font, `Artex` is the UI font
- `#ebff52` yellow-green is the nav bar color and primary accent — use it deliberately
- The status pill ("Default Alive ✓" / "Default Dead ✗") is the emotional centrepiece — make it impossible to miss
