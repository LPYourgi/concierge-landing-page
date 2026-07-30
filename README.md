# Concierge Landing Page ("Find me a sitter")

A standalone flat-rate concierge landing page — visitor picks a service, gets an upfront flat price, and submits a request; concierge follows up by text and books manually. No platform integration. Tests whether customers accept a flat-rate, "we'll find the pro for you" model.

**New here? → Read [`docs/handoff.md`](docs/handoff.md) first.**

## Files

- `find-me-a-sitter.html` — the clickable prototype (canonical, icon service options). Double-click to open.
- `deploy/index.html` — identical copy named `index.html`, ready to drop into a static host.
- `docs/handoff.md` — start-here onboarding for a new designer.
- `docs/project-context.md` — full 8-section project context.
- `docs/PRD.md` — partial PRD (⚠️ items are unresolved).
- `docs/kai-message-draft.md` — draft message to Kai on the open decisions.

**Figma:** https://www.figma.com/design/VFo9u0adaFx7ju9wfy45Hj

## Open decisions (confirm before a real build)

| # | Decision | Owner |
|---|----------|-------|
| 1 | Rate set ($50/$40/$20 vs $50/$44/$24) + fee rounding | Kai |
| 2 | Customer response-time SLA | Chris → Kai |
| 3 | Yourgi Guarantee wording | Legal / Kai |
| 4 | Where form submissions land — **blocks build** | Kai / Jeff |
| 5 | Phone-only contact (email removed) — confirm | Lauren / Kai |
| 6 | National 2 font + official logo lockup | Webflow / brand |

## Team

Lauren Palma (lead) + Rikki Mortimore (design). Jeff owns form destination + downstream booking. Chris confirms the open items with Kai.

---
_Reopen by reconnecting the `Yourgi Projects` folder; read `docs/handoff.md` first._
