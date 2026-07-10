# Goal 001 — Ledger v0

**Status:** DONE (2026-07-10)
**Milestone:** [M1 — Ledger v0](../entities/roadmap.md)
**Stop clause:** max 15 worker cycles, or 2 consecutive no-progress cycles →
set Status: BLOCKED and write exactly why below.

## Demo (what "works" looks like)
A user can create a chart of accounts, upload a bank statement CSV, categorize the imported transactions, and see a correct Balance Sheet and P&L in the browser — all on a local machine.

## Done when
- [x] The app skeleton exists (Next.js + TypeScript + Prisma + Postgres per [stack.md](../entities/stack.md)) and the gate command runs the full chain — build, lint, unit tests, Playwright e2e — failing loudly if any stage fails (verified by: `npm run gates` in the code repo)
- [x] The double-entry posting engine stores money as integer cents, rejects any transaction whose debits ≠ credits, and keeps the trial balance at exactly zero across a randomized batch of valid postings (verified by: `npm test` — `posting-engine.spec.ts`)
- [x] A user can create, rename, and deactivate accounts in a chart of accounts, choosing one of the five types (Asset, Liability, Equity, Income, Expense), and the list survives a page reload (verified by: Playwright `e2e/chart-of-accounts.spec.ts`)
- [x] A user can upload the sample bank-statement CSV (fixture committed in the code repo at `fixtures/sample-bank-statement.csv`) and see every row appear as an uncategorized bank transaction with date, description, and amount intact (verified by: Playwright `e2e/import.spec.ts`)
- [x] Re-uploading the same CSV does not create duplicate transactions, and the user sees a message saying how many rows were skipped (verified by: Playwright `e2e/import.spec.ts`)
- [x] A user can assign an uncategorized transaction to an account, which posts a balanced ledger entry (bank account ↔ chosen account) and moves it to the categorized list (verified by: Playwright `e2e/categorize.spec.ts`)
- [x] The Balance Sheet page shows Assets, Liabilities, and Equity computed from posted entries, and Assets = Liabilities + Equity on screen for the fixture data (verified by: Playwright `e2e/reports.spec.ts`)
- [x] The P&L page shows Income, Expenses, and Net Income for a selectable date range, matching hand-computed totals for the fixture data (verified by: unit test `reports.spec.ts` + Playwright `e2e/reports.spec.ts`)
- [x] All of the above pass together from a clean checkout (verified by: `npm run gates`)

## Waiting on Chris
- (Optional, not blocking) A real bank-statement CSV export from TFA's bank, so the import format matches reality. Synthetic fixture is used until then. **Redact/replace anything sensitive before committing it.**

## Out of scope (goes to roadmap, not code)
- Login/auth and Railway deployment (M2) · Cash Flow statement (M3) · bank feeds, duplicate rules, reconciliation (M4) · journal-entry UI, invoicing (M5) · multi-entity (M6)

## Iteration log
- 2026-07-10 factory: goal drafted at project birth. No cycles run yet.
- 2026-07-10 worker (cycle 1): built the whole goal in one session — skeleton (Next.js 15 + TS + Prisma 6 + Postgres 16), posting engine + 33 unit tests, chart of accounts, CSV import with dedupe, categorization, balance sheet + P&L, 15 Playwright tests. `npm run gates` green end to end. Code commit `9649ab5`.
- 2026-07-10 worker (cycle 1, cont.): clean-checkout verification — fresh clone, `npm ci`, empty `tfa_quickbooks_test` database, `npm run gates` → exit 0, 15/15 e2e passed.
- 2026-07-10 architect: gate falsification — removed the debits≠credits check → `posting-engine.spec.ts` FAILED (good); salted the dedupe hash → `e2e/import.spec.ts` re-upload test FAILED (good); both restored, gates green. Adversarial review (fresh agent context; same model as worker — no other model available in this environment, noted as a deviation from the preference) found 1 critical + 7 lesser issues.
- 2026-07-10 worker (cycle 2): review fixes — categorization race (guarded updateMany; reproduced then locked in by `e2e/integrity.spec.ts` concurrency test, which FAILS against the pre-fix code), decimal-comma amount rejection, zero-amount rows ignored at import with visible count, strict report dates, CSV space-before-quote, P2025 handling, DB CHECK constraints + case-insensitive account uniqueness (migration `20260710220306`). Gates: 35 unit + 22 e2e green. Commit `c5f0401`.
- 2026-07-10 architect: transfer double-counting (review finding 4) deferred to M4 with a documented convention — see [../concepts/transfers-double-count.md](../concepts/transfers-double-count.md) and decision D-007. Verification ratchet satisfied: gates grew from 33 unit + 15 e2e to 35 unit + 22 e2e, now covering concurrency, DB-level invariants, malformed amounts/dates, and zero rows. **Goal closed.**
