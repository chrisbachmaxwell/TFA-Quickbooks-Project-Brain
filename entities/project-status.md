# Project status

**As of 2026-07-10 (evening) — Ledger v0 built and reviewed; UI rebuilt to Wave/QBO standard. Not yet deployed.**

## What works (all proven by `npm run gates`: 42 unit + 26 Playwright browser tests)
- Chart of accounts: create / rename / deactivate, five types, case-insensitive unique names.
- Bank-statement CSV import with dedupe (re-uploads skip; zero-amount rows ignored with a visible count; malformed files rejected with row numbers).
- Categorization of imported transactions into balanced double-entry journal postings (integer cents; concurrency-safe; DB CHECK constraints as backstop).
- Balance Sheet (with as-of date) and P&L (with date range) — totals verified against hand-computed fixtures; invalid dates error instead of rendering an empty "balanced ✓" report.

## Where things stand
- **Goal 001 (Ledger v0): DONE** — see its iteration log for the adversarial review + gate falsification record. Code repo commits `9649ab5`, `c5f0401`.
- **Active goal: [../goals/003-wave-quality-ui.md](../goals/003-wave-quality-ui.md) (IN PROGRESS)** — inserted by Chris's feedback. All build items done and gated (commit `62cef49`: sidebar shell, dashboard with KPIs + monthly chart, statement-styled reports); the one open box is Chris's visual sign-off.
- **Next goal: [../goals/002-deployed-and-private.md](../goals/002-deployed-and-private.md) (PLANNED)** — Railway deploy, login, backups; has "Waiting on Chris" items (Railway project + app password).
- **Known limitation (by decision D-007):** bank-to-bank transfers must only be categorized on one side until M4 — [../concepts/transfers-double-count.md](../concepts/transfers-double-count.md).
- **No real financial data in the app yet** — that waits for M2's login + deployment, per decision D-005.
- Everything lives on git branch `claude/project-factory-setup-rz0utl` (GitHub made it the default branch since the repos started empty).

## Next action
Chris signs off (or not) on the new UI → goal 003 closes → a worker starts goal 002 (auth + backup script + deploy config are all local work).
