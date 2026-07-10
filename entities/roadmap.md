# Roadmap

Milestones in order. One active goal at a time; the architect drafts the next goal page when one closes. Out-of-scope ideas land here, never in code.

## M1 — Ledger v0 ✅ DONE 2026-07-10
Goal page: [../goals/001-ledger-v0.md](../goals/001-ledger-v0.md)
A user can create a chart of accounts, upload a bank statement CSV, categorize the imported transactions, and see a correct Balance Sheet and P&L in the browser. Shipped with 35 unit + 22 Playwright tests via `npm run gates`.

## M1.5 — Wave-quality UI ✅ DONE 2026-07-10
Goal page: [../goals/003-wave-quality-ui.md](../goals/003-wave-quality-ui.md)
Dashboard with KPIs and a monthly chart, sidebar app shell, statement-styled reports. Chris signed off same day.

## THE PARITY RUN (authorized by Chris 2026-07-10: "add as many goals as you want… do all the tasks until it is done")
Executed in this order, one goal at a time, gates green between each:
1. [goals/002](../goals/002-deployed-and-private.md) — login auth, backups, Railway deploy config
2. [goals/004](../goals/004-cash-flow-statement.md) — Cash Flow statement (completes Chris's three reports)
3. [goals/005](../goals/005-manage-transactions.md) — undo, exclude, manual journal entries
4. [goals/006](../goals/006-split-transactions.md) — split categorization
5. [goals/007](../goals/007-registers-and-ledger-reports.md) — account registers, trial balance, general ledger, reports hub
6. [goals/008](../goals/008-categorization-qol.md) — suggestions, bulk categorize, starter chart of accounts
7. [goals/009](../goals/009-transfer-matching.md) — transfer matching (retires D-007)
8. [goals/010](../goals/010-report-exports-and-comparison.md) — CSV exports, P&L comparison, date presets

## M2 — Deployed and private
Goal page: [../goals/002-deployed-and-private.md](../goals/002-deployed-and-private.md)
The app runs on Railway with managed Postgres, behind a login (single user is fine), with automated database backups verified restorable. TFA's real books can start living in it.

## M3 — Cash Flow statement
The third of Chris's three reports, with tests proving it reconciles against the ledger (indirect method first).

## M4 — Bank connection & smarter import
Direct bank feed (e.g. Plaid or similar aggregator — evaluate cost/privacy first) or a polished recurring-statement-upload flow; duplicate detection; categorization rules/memory ("this payee → this account"); bank reconciliation workflow; **transfer matching between own bank accounts** (v0 double-counts if both sides are categorized — see [../concepts/transfers-double-count.md](../concepts/transfers-double-count.md)).

## M5 — The rest of a real accounting package
Manual journal entries UI, invoicing / accounts receivable, bills / accounts payable, document attachments, report export (PDF/CSV), period close.

## M6 — Multi-entity
TFA is a holding company: multiple sets of books (per business/investment) under one roof, with consolidated reporting.

## Parking lot
(Ideas that don't have a milestone yet — add here, dated.)
