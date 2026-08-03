# Handoff — Concierge Landing Page ("Best Care Guarantee")

**For:** Rikki Mortimore · **From:** Lauren Palma · **Last updated:** 30 July 2026

Read this first. It's the one doc that gets you oriented; the others (`project-context.md`, `PRD.md`) go deeper.

---

## What this is

A standalone, flat-rate concierge landing page — a deliberately "fake front end" (Chris's word: *Potemkin*). The visitor picks a service, gets an upfront flat price, and submits a request; a real person on the concierge team follows up by text and books it manually. There's no platform integration behind it. The whole point is a cheap test of one question: **will customers accept a flat-rate, "we'll find the pro for you" model for pet care?**

Target page: something like `yourgi.com/book/best-care-guarantee` (renamed from `find-a-pro` on 2026-07-31), separate from the homepage. Original timeline was end of week.

## Current status

Interactive HTML prototype is **built, tested, and on-brand**, and the matching Quote flow is in Figma. It is **not** production. As of 2026-07-30, submissions POST to a Power Automate webhook into the concierge team's Teams channel (fire-and-forget, no confirmation read back) — a working stopgap, not a confirmed permanent destination. Several values are deliberate placeholders pending Kai/legal (see "Open items" below). Think of it as a clickable, reviewable spec — not a finished page.

## Where everything lives

```
Concierge Landing Page/
├── README.md                  ← folder index
├── best-care-guarantee.html   ← THE prototype (canonical, icon service options). Double-click to open.
├── index.html                 ← identical copy for GitHub Pages (serves from repo root)
├── deploy/
│   └── index.html             ← identical copy named index.html, ready to drop into a static host
└── docs/
    ├── handoff.md             ← you're reading it
    ├── project-context.md     ← full 8-section project context (problem, ICP, constraints, gaps)
    ├── PRD.md                 ← partial PRD (what to build; ⚠️ items are unresolved)
    └── kai-message-draft.md   ← draft message to Kai on the open decisions
```

**Figma (design source):** https://www.figma.com/design/VFo9u0adaFx7ju9wfy45Hj — the "1 · Quote" frame matches the prototype; "2 · Confirmation" and "3 · Out of market" show the other states.

## How to open / run the prototype

Double-click `best-care-guarantee.html` — it opens in any browser, no setup. Be online the first time so the Yourgi logo and fonts load from the CDN (offline, the logo falls back to a "YOURGI" wordmark). Try it end to end: pick a service, open the **Dates** field and choose a range, adjust pets, enter a zip and phone, then **Find my pro**. Test both a covered zip (e.g. 80202) and an out-of-market one (e.g. 90210) to see both end states.

It's a single self-contained file — all CSS and JS are inline. The logic was pressure-tested headlessly (34 checks, all passing): quote math, calendar range, zip/phone validation, and all routing.

## Decisions already made

- **Quote-first, not calendar-first** — price shows up front (the model being tested), matching the Handy pattern Chris referenced.
- **Icon service options** — Boarding / Daycare / House sitting / Dog walking as icon tiles (Phosphor icons, brand circle colors), scoped to pro services only.
- **Single "Select your dates" field** with a calendar popover (matches the live yourgi.com widget); nights derive from the range.
- **Phone + zip captured up front**; the flow completes in one step (no separate name/email screen). Location routing is driven by the zip.
- **Rates shown, coupon disclaimer present, rewards line removed** from the quote card (the 5%-back program is real but its application to a flat-rate booking isn't confirmed).
- **Voice + visuals** follow the `yourgi-brand` skill; copy uses approved headlines and the covered markets (Denver, Dallas, Fort Worth, Houston, Boston, Portland).

## Open items — pending, do not treat as final

| # | Item | Owner |
|---|------|-------|
| 1 | Correct rate set — **$50/$40/$20** vs **$50/$44/$24** — and whether the 5% fee is rounded into the displayed price | Kai |
| 2 | Customer response-time commitment (prototype shows a placeholder "within an hour, 8am–8pm MT") | Chris → Kai |
| 3 | Yourgi Guarantee wording — legal boundaries undocumented; current copy is light and flagged | Legal / Kai |
| 4 | Where form submissions land — wired to Power Automate → Teams channel as of 2026-07-30 (Jeff's suggested option, simplest); still needs Kai's sign-off as the permanent destination. Note: the webhook URL is hardcoded client-side and unauthenticated — anyone who views source can POST to it, so this should be revisited before the page carries real ad traffic | Kai / Jeff |
| 5 | ~~Phone-only contact (email was removed)~~ — resolved: email was re-added as a required field alongside phone | Lauren |
| 6 | National 2 font + official logo lockup — prototype uses Oswald/Archivo stand-ins and the CDN logo | Webflow team / brand |

## How to edit

- **Prototype:** open `best-care-guarantee.html` in any code editor. It's plain HTML/CSS/JS, no build step. Keep both the `deploy/index.html` copy and the root `index.html` (GitHub Pages) in sync if you change the canonical file.
- **Design:** edit in the Figma file above. Ask Lauren to add you with edit access.
- **Copy / brand:** run anything customer-facing through the `yourgi-brand` skill; keep placeholders labeled until Kai/legal confirm.

## Suggested next steps for Rikki

1. Open the prototype and click through both end states.
2. Skim `project-context.md` and `PRD.md` for the full picture.
3. Get the open items above answered (they gate a real build) — the `kai-message-draft.md` is a starting point.
4. When decisions land, update this doc and `project-context.md` so it stays the current record.

Questions → Lauren Palma (lauren.palma@destpet.com).
