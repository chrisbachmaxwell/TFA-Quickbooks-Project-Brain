# Goal 003 — A UI worth trusting your books to (Wave/QBO-quality)

**Status:** DONE (2026-07-10)
**Milestone:** inserted ahead of M2 by Chris's direct feedback 2026-07-10: "it looks pretty rough and simple.. can you make this as good as quickbooks or at least wave accounting?"
**Stop clause:** max 10 worker cycles, or 2 consecutive no-progress cycles →
set Status: BLOCKED and write exactly why below.

## Demo (what "works" looks like)
Opening the app feels like opening Wave: a real dashboard greets you with your cash position, income/expenses/net for the year, a monthly income-vs-expenses chart, and a "transactions to review" prompt. A proper sidebar navigates to Banking (import, review), Accounting (chart of accounts), and Reports. Financial statements look like statements — company header, sections, indents, rules under totals — not bare tables.

## Done when
- [x] A dashboard at `/` shows KPI tiles — cash balance, YTD income, YTD expenses, YTD net income — whose figures match the fixture's hand-computed totals, plus a count of transactions waiting for review that links to the review screen (verified by: Playwright `e2e/dashboard.spec.ts`)
- [x] The dashboard renders a monthly income-vs-expenses bar chart computed from posted ledger entries; the month-bucketing math is unit-tested against the fixture, and the chart carries a legend and an accessible data table (verified by: `npm test` — `dashboard.spec.ts` + Playwright `e2e/dashboard.spec.ts`)
- [x] Every page shares an app shell: brand sidebar with grouped navigation (Dashboard / Banking / Accounting / Reports) and an active-page indicator (verified by: Playwright `e2e/dashboard.spec.ts` nav assertions)
- [x] Chart of accounts is grouped into sections by account type with styled type badges and status badges; transactions show money-in amounts in green with the review flow presented as "For review" / "Categorized"; reports are formatted as financial statements (company header, date line, indented rows, ruled totals) (verified by: existing Playwright suites still passing unchanged — `npm run gates` — plus new DOM assertions in `e2e/dashboard.spec.ts`)
- [x] No regression anywhere: the full existing gate suite passes without modifying any existing test's assertions except where counts grow (verified by: `npm run gates`)
- [x] Chris looks at fresh screenshots and agrees it clears the "Wave or better" bar — his call, recorded here (verified by: Chris's reply in session — 2026-07-10: "yes go for it")

## Waiting on Chris
- ~~Final visual sign-off~~ received 2026-07-10.

## Out of scope (goes to roadmap, not code)
- New accounting features (this goal changes presentation, not the ledger)
- Dark mode, mobile app shell (parking lot)
- Deployment/auth — still goal 002, next after this

## Iteration log
- 2026-07-10 architect: drafted from Chris's feedback; supersedes goal 002 as active until closed.
- 2026-07-10 worker (cycle 1): app shell with sidebar nav, dashboard (KPI tiles + review callout + monthly income-vs-expenses SVG chart, palette validated with the dataviz six-checks script), accounts grouped by type with badges, banking-style review screen, statement-formatted reports. New gates: `lib/dashboard.spec.ts` (7 unit tests) + `e2e/dashboard.spec.ts` (4 browser tests). All existing suites pass unchanged except one row-count that legitimately grew. Gates: 42 unit + 26 e2e green. Commit `62cef49`.
- 2026-07-10 architect: eyeballed rendered output per the dataviz method; caught non-round y-axis ticks ($625/$1.9k) and replaced the scale with 1/2/5-step ticks before shipping. Screenshots sent to Chris; his sign-off is the one open box.
- 2026-07-10 architect: Chris signed off ("yes go for it"). Goal closed. He also authorized a long autonomous run toward full Wave/QBO parity — goals 004-010 drafted, goal 002 re-queued first.
