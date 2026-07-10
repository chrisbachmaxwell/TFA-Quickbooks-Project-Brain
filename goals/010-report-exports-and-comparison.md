# Goal 010 — Report exports, P&L comparison, date presets

**Status:** PLANNED
**Milestone:** part of M5, pulled forward
**Stop clause:** max 6 worker cycles, or 2 no-progress cycles → BLOCKED with reasons.

## Demo (what "works" looks like)
Every statement has a "Download CSV" button whose file matches the screen. The P&L can show a second column for the previous period with a change column. Date pickers have one-click presets (This month / This quarter / This year / Last year).

## Done when
- [ ] Balance Sheet, P&L, Cash Flow, and Trial Balance each export CSV via a download link on the page; the CSV's totals equal the rendered totals (verified by: Playwright `e2e/exports.spec.ts` — downloads parsed and asserted against fixture numbers)
- [ ] P&L supports `compare=previous`: a prior-period column of equal length plus a change column, each row aligned by account (verified by: unit test `comparison.spec.ts` + Playwright `e2e/exports.spec.ts`)
- [ ] Report date controls offer This month / This quarter / This year / Last year presets that set the from/to fields (verified by: Playwright `e2e/exports.spec.ts`)
- [ ] All gates green (verified by: `npm run gates`)

## Waiting on Chris
- (nothing)

## Out of scope
- PDF export (print styles already exist; browser print-to-PDF is the v1 answer)

## Iteration log
- 2026-07-10 architect: drafted for the long autonomous run.
