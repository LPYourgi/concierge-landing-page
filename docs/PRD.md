# PRD (Partial): Concierge Landing Page — Flat-Rate Test
**Date:** 29 July 2026 · **Version:** 0.1 (draft) · **Owner:** Lauren + Ree (build), Jeff (form + downstream)
**Status:** Partial — sections marked ⚠️ are blocked on decisions in `README.md` / `project-context.md §7`.

> Companion to `docs/project-context.md`. This PRD says what to build; the context doc says why and tracks the gaps. Chris is also sending his own written notes + partial PRD to the Teams channel — reconcile when they land.

---

## 1. Summary
A single, standalone Webflow landing page (a deliberately "Potemkin" front end) that lets a pet parent describe a service, get an instant flat-rate quote, and submit a request. No platform integration: the submission goes to the concierge team, who follow up by text (SendBlue) and create the booking manually. Goal is a cheap test — roughly half a day of build — of whether customers accept a flat-rate, concierge-matched model.

## 2. Goals / Non-goals
**Goals**
- Ship a quote-first landing page at a URL like `yourgi.com/find-me-a-sitter` by Friday.
- Capture qualified requests with enough info for concierge to follow up and book.
- Match the Yourgi brand style guide (follows the `yourgi-brand` skill).

**Non-goals**
- No live matching, provider browsing, or account creation on the page.
- No platform/API integration for booking (concierge does it by hand).
- No Geo-IP gating.

## 3. User flow
1. User lands on the page (from a Kai-run geo-targeted ad).
2. User enters: service type, dates, number of pets, location/city, phone (required), email (required).
3. User taps "Get a Price" → sees an instant flat-rate estimated total (base rate × inputs + 5% fee).
4. User submits the request.
5. Confirmation screen: no live match; sets explicit response-time expectation; states a human will reach out and connect them with a pro.
6. Behind the scenes: submission routes to concierge ⚠️(destination TBD) → concierge texts via SendBlue → booking created manually.

## 4. Page structure
- **Above the fold:** headline + the quote widget (inputs → Get a Price → flat quote). Recurring-plan discount hook lives in the same widget.
- **Below the fold:** trust signals — guarantee, vetted pros, 24/7 support, review volume. These are reassurance, not a selection step.
- **Footer:** standard content.

## 5. Fields to collect
| Field | Required | Notes |
|-------|----------|-------|
| Service type | Yes | Boarding, house sitting, daycare, dog walking |
| Dates | Yes | Drives the quote (nights / days) |
| Number of pets | Yes | Drives the quote |
| Location / city | Yes | Also gates in/out-of-market messaging |
| Phone | Yes | Concierge texts via SendBlue |
| Email | Yes | — |

Inputs as form fields or buttons — team's call.

## 6. Pricing & quote logic
Base rates (⚠️ confirm set + fee-rounding with Kai before building — see §Open):

| Service | Rate |
|---------|------|
| Boarding | $50 / night |
| House sitting | $50 / night |
| Daycare | $40 / dog / day |
| Dog walking | $20 / 30 min |

- Estimated total = base rate applied to inputs (e.g. 2 nights × 2 dogs, boarding) **+ 5% fee**.
- ⚠️ Unresolved: rates were also restated as "$50 / $44 / $24" — either base+fee or a transcription artifact. Confirm which set displays and whether the fee is rounded into the shown price.
- Coupon disclaimer: coupons not valid with this flat-rate offer.

## 7. Copy requirements
- Names the covered markets in-copy (⚠️ specific markets not yet provided — ask Kai).
- Out-of-market submission → "thanks for the interest, we're not there yet" (possibly saved as a lead).
- Confirmation must set a concrete response-time expectation — avoid the vague "we'll reach out" failure mode (the car-shipping analogy). Concierge is staffed US business hours; realistic turnaround an hour or two, off-hours waits.
- Yourgi Guarantee messaging kept light, with layout space reserved for Kai's web devs to expand. ⚠️ Guarantee wording needs review before publish (undocumented legal boundaries).
- All copy follows the `yourgi-brand` skill.

## 8. Technical
- **Platform:** Webflow (default; copy an existing landing page as a starting point). Vibe coding with Claude encouraged.
- **Form destination:** Wired as of 2026-07-30 to Power Automate → Teams channel (Jeff's instinct, simplest) as a stopgap. ⚠️ Still needs Kai's sign-off as the permanent destination; the webhook URL is currently hardcoded client-side with no auth, which should be revisited before real ad traffic hits the page.
- **Downstream booking:** ⚠️ Jeff to define how concierge creates the booking, including making an account for account-less customers and "masquerading" into it.
- **Publishing:** heads-up to Paul & Mike before publishing; Lauren/Alex publish to staging regularly, so no obvious conflict — flag anyway. Lauren still needs Webflow access (Chris → Carlos).
- **Longer term:** move off the Webflow MCP toward Storyblok so the site can be fully coded (out of scope for this test).

## 9. Open items before build
1. Form destination + owner of that pipe (Kai / Jeff) — wired to Power Automate → Teams as a stopgap 2026-07-30; still needs Kai's sign-off + a non-hardcoded webhook before real traffic.
2. Correct rate set + whether prices are fee-inclusive (Kai).
3. Customer response-time SLA (Chris → Kai).
4. Booking creation for account-less customers (Jeff).
5. Keep out-of-market submissions as leads, or discard.
6. Specific covered markets to name in copy (Kai).

## 10. Milestone
Single milestone: **page live by Friday.** No phased rollout defined.
