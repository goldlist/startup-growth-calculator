# TechTO Startup Growth Calculator

A modern, mobile-first reimagining of Trevor Blackwell's startup funding calculator — branded for TechTO and built for Canadian founders.

**Live:** [growth.techto.org](https://growth.techto.org) *(coming soon)*

---

## What it does

Enter your monthly revenue, expenses, growth rate, and cash on hand. The calculator tells you whether you're **Default Alive** (you'll reach profitability before running out of money) or **Default Dead** (you won't) — and shows you exactly how far away you are from each outcome.

Concept from Paul Graham's essay: [Default Alive or Default Dead?](https://www.paulgraham.com/aord.html)

---

## Inspiration & Attribution

This project is inspired by **[Trevor Blackwell's startuptools](https://gitlab.com/tlb/startuptools)** (MIT License). The core math model — exponential revenue growth against flat expenses — comes from his original calculator at [growth.tlb.org](https://growth.tlb.org).

We built a new frontend from scratch (React + Tailwind, TechTO brand), but the underlying idea and formulas are his. Credit where it's due.

---

## Stack

- React 18 (via CDN, no build step)
- Tailwind CSS (via CDN)
- Pure SVG chart
- URL-encoded state (shareable links, no backend)
- Webflow CSS/JS for nav and brand components

## Running locally

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080`.

---

*Built by [TechTO](https://techto.org) for Canadian founders.*
