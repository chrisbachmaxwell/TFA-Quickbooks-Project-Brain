# Roadmap

Milestones in order. One active goal at a time; the architect drafts the next goal page when one closes. Out-of-scope ideas land here, never in code.

## M1 — Ledger v0 ← ACTIVE
Goal page: [../goals/001-ledger-v0.md](../goals/001-ledger-v0.md)
A user can create a chart of accounts, upload a bank statement CSV, categorize the imported transactions, and see a correct Balance Sheet and P&L in the browser. Runs locally; all gates runnable.

## M2 — Deployed and private
The app runs on Railway with managed Postgres, behind a login (single user is fine), with automated database backups verified restorable. TFA's real books can start living in it.

## M3 — Cash Flow statement
The third of Chris's three reports, with tests proving it reconciles against the ledger (indirect method first).

## M4 — Bank connection & smarter import
Direct bank feed (e.g. Plaid or similar aggregator — evaluate cost/privacy first) or a polished recurring-statement-upload flow; duplicate detection; categorization rules/memory ("this payee → this account"); bank reconciliation workflow.

## M5 — The rest of a real accounting package
Manual journal entries UI, invoicing / accounts receivable, bills / accounts payable, document attachments, report export (PDF/CSV), period close.

## M6 — Multi-entity
TFA is a holding company: multiple sets of books (per business/investment) under one roof, with consolidated reporting.

## Parking lot
(Ideas that don't have a milestone yet — add here, dated.)
