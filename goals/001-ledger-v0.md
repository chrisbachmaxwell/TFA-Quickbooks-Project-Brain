# Goal 001 — Ledger v0

**Status:** PLANNED
**Milestone:** [M1 — Ledger v0](../entities/roadmap.md)
**Stop clause:** max 15 worker cycles, or 2 consecutive no-progress cycles →
set Status: BLOCKED and write exactly why below.

## Demo (what "works" looks like)
A user can create a chart of accounts, upload a bank statement CSV, categorize the imported transactions, and see a correct Balance Sheet and P&L in the browser — all on a local machine.

## Done when
- [ ] The app skeleton exists (Next.js + TypeScript + Prisma + Postgres per [stack.md](../entities/stack.md)) and the gate command runs the full chain — build, lint, unit tests, Playwright e2e — failing loudly if any stage fails (verified by: `npm run gates` in the code repo)
- [ ] The double-entry posting engine stores money as integer cents, rejects any transaction whose debits ≠ credits, and keeps the trial balance at exactly zero across a randomized batch of valid postings (verified by: `npm test` — `posting-engine.spec.ts`)
- [ ] A user can create, rename, and deactivate accounts in a chart of accounts, choosing one of the five types (Asset, Liability, Equity, Income, Expense), and the list survives a page reload (verified by: Playwright `e2e/chart-of-accounts.spec.ts`)
- [ ] A user can upload the sample bank-statement CSV (fixture committed in the code repo at `fixtures/sample-bank-statement.csv`) and see every row appear as an uncategorized bank transaction with date, description, and amount intact (verified by: Playwright `e2e/import.spec.ts`)
- [ ] Re-uploading the same CSV does not create duplicate transactions, and the user sees a message saying how many rows were skipped (verified by: Playwright `e2e/import.spec.ts`)
- [ ] A user can assign an uncategorized transaction to an account, which posts a balanced ledger entry (bank account ↔ chosen account) and moves it to the categorized list (verified by: Playwright `e2e/categorize.spec.ts`)
- [ ] The Balance Sheet page shows Assets, Liabilities, and Equity computed from posted entries, and Assets = Liabilities + Equity on screen for the fixture data (verified by: Playwright `e2e/reports.spec.ts`)
- [ ] The P&L page shows Income, Expenses, and Net Income for a selectable date range, matching hand-computed totals for the fixture data (verified by: unit test `reports.spec.ts` + Playwright `e2e/reports.spec.ts`)
- [ ] All of the above pass together from a clean checkout (verified by: `npm run gates`)

## Waiting on Chris
- (Optional, not blocking) A real bank-statement CSV export from TFA's bank, so the import format matches reality. Synthetic fixture is used until then. **Redact/replace anything sensitive before committing it.**

## Out of scope (goes to roadmap, not code)
- Login/auth and Railway deployment (M2) · Cash Flow statement (M3) · bank feeds, duplicate rules, reconciliation (M4) · journal-entry UI, invoicing (M5) · multi-entity (M6)

## Iteration log
- 2026-07-10 factory: goal drafted at project birth. No cycles run yet.
