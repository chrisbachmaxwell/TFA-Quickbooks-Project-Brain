# Goal 004 — Cash Flow statement

**Status:** PLANNED
**Milestone:** [M3 — Cash Flow statement](../entities/roadmap.md)
**Stop clause:** max 8 worker cycles, or 2 no-progress cycles → BLOCKED with reasons.

## Demo (what "works" looks like)
Chris opens Reports → Cash Flow, picks a period, and sees where cash came from and went — Operating / Investing / Financing sections, net change in cash, and beginning → ending cash that reconciles exactly with the balance sheet's cash.

## Done when
- [ ] Accounts carry a **cash account** flag (bank/cash assets); imports are restricted to cash accounts; the accounts UI can set the flag; existing ASSET accounts with imported transactions are backfilled as cash by migration (verified by: `npm run gates` — migration applies + `e2e/cash-flow.spec.ts`)
- [ ] A pure `cashFlow(accounts, entries, from, to)` classifies every journal entry that touches a cash account by its non-cash side — INCOME/EXPENSE → Operating, non-cash ASSET → Investing, LIABILITY/EQUITY → Financing — and returns sections, net change, beginning and ending cash (verified by: `npm test` — `cash-flow.spec.ts`, fixture: operating 5,324.50 / financing 10,000.00 / net change 15,324.50)
- [ ] `/reports/cash-flow` renders it statement-styled with from/to controls, and ending cash equals the balance sheet's cash total for the same as-of date (verified by: Playwright `e2e/cash-flow.spec.ts`)
- [ ] Sub-period beginning cash is the cash balance the instant before `from` (verified by: unit test `cash-flow.spec.ts` — Feb-only period: beginning 2,410.75 / net change 1,185.00 / ending 3,595.75)
- [ ] All gates green (verified by: `npm run gates`)

## Waiting on Chris
- (nothing)

## Out of scope
- Accrual adjustments (no AR/AP yet) · multi-entity

## Iteration log
- 2026-07-10 architect: drafted for the long autonomous run.
