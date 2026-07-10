# Goal 007 — Account registers, trial balance, general ledger, reports hub

**Status:** DONE (2026-07-10)
**Milestone:** part of M5, pulled forward
**Stop clause:** max 8 worker cycles, or 2 no-progress cycles → BLOCKED with reasons.

## Demo (what "works" looks like)
Clicking any account opens its register — every posting that touched it, QuickBooks-style, with date, memo, the other side, debit/credit, and a running balance. Reports has its own hub page, and an accountant can pull a trial balance and a general ledger.

## Done when
- [x] Every account name on the chart of accounts links to `/accounts/[id]` — a register of that account's journal lines (date, memo, other account(s), debit, credit, running balance), oldest first, with the final running balance equal to the account's report balance (verified by: Playwright `e2e/registers.spec.ts`, fixture: TFA Checking ends at 15,324.50)
- [x] `/reports/trial-balance?asOf=` lists every account with a nonzero balance in debit/credit columns; total debits equal total credits on screen (verified by: Playwright `e2e/registers.spec.ts` + unit test `trial-balance.spec.ts`)
- [x] `/reports/general-ledger?from=&to=` shows each account's lines and period totals, statement-styled (verified by: Playwright `e2e/registers.spec.ts`)
- [x] `/reports` is a hub page linking Balance Sheet, P&L, Cash Flow, Trial Balance, General Ledger, each with a one-line description; the sidebar Reports section routes through it (verified by: Playwright `e2e/registers.spec.ts`)
- [x] All gates green (verified by: `npm run gates`)

## Waiting on Chris
- (nothing)

## Out of scope
- Editing from the register · pagination (fine until books are much bigger)

## Iteration log
- 2026-07-10 architect: drafted for the long autonomous run.
- 2026-07-10 worker (cycle 1): built as specced; gates 59 unit + 52 e2e green first run. Commit `dcf9485`.
