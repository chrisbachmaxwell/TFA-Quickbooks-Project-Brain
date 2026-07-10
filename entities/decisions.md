# Decisions

Decisions made, with reasons. Check here before re-deciding anything. To reverse one: add a new dated entry that supersedes it — don't silently rewrite history.

## D-001 · 2026-07-10 · Stack: Next.js + TypeScript + Prisma + PostgreSQL
Chris said "you choose, we will be hosting it on Railway." Next.js gives one deployable codebase for UI and API on Railway; Prisma+Postgres is the most well-trodden path for it, which matters because AI agents build this — boring, heavily documented choices reduce agent error rates. Vitest for unit tests, Playwright for browser gates.

## D-002 · 2026-07-10 · Postgres everywhere (no SQLite dev shortcut)
One database engine in dev, test, and prod. Financial data on Railway gets managed Postgres (backups); mixing SQLite locally with Postgres in prod invites dialect bugs in the one place we can't afford them — the ledger.

## D-003 · 2026-07-10 · Money is integer cents
No floating point anywhere near amounts. Non-negotiable for accounting software.

## D-004 · 2026-07-10 · Real double-entry from day one
Not a transaction list with reports bolted on. Balance Sheet/P&L/Cash Flow are only trustworthy if every transaction posts balanced debits and credits, so the posting engine comes first and is the most tested code in the app.

## D-005 · 2026-07-10 · v0 is local-only; deployment and auth are M2
Keeps goal 001 small enough to finish. No real financial data goes into the app until it's deployed behind a login (M2).

## D-006 · 2026-07-10 · CSV upload before bank feeds
Statement upload is fully under our control and testable with fixtures. Direct bank connections (Plaid etc.) involve cost/privacy trade-offs — deferred to M4 with an explicit evaluation step.

## D-007 · 2026-07-10 · Transfer matching deferred to M4; one-sided convention until then
Adversarial review showed categorizing both sides of a bank-to-bank transfer double-counts it (see [../concepts/transfers-double-count.md](../concepts/transfers-double-count.md)). Real matching is M4 scope; until then the convention is: categorize only the sending side, leave the mirror row uncategorized.

## D-008 · 2026-07-10 · The database enforces ledger invariants too, not just code
CHECK constraints (non-negative, one-sided journal lines) and case-insensitive unique account names live in the schema itself, so no future write path can silently corrupt the books. Any new invariant the code enforces should get a DB-level backstop where Postgres can express it cheaply.

## D-009 · 2026-07-10 · Invoicing/AR deliberately parked
Wave's other half is invoicing, but TFA is a holding company — dividends, transfers, and expenses dominate; nobody sends TFA-branded invoices. Building it well needs Chris's requirements (branding, delivery, tax). Parked on the roadmap parking lot until he asks; the parity run spends that effort on books-quality instead (registers, journal entries, transfers, cash flow).
