# Vision

**TFA-Quickbooks** is a self-hosted accounting application that replaces QuickBooks for **TFA**, a holding company that holds shares of businesses as well as other investments. The point is to stop paying for QuickBooks while keeping (and eventually customizing) everything a good accounting package does.

## Who it's for
Chris and TFA internally. One company's books first; a holding company holds multiple entities, so multi-entity support is on the roadmap, not in v0.

## Must-haves (from Chris, 2026-07-10)
1. **Chart of accounts** — create and manage a full chart of accounts.
2. **Bank data in** — connect to a bank account, or at minimum upload bank statements; statements become transactions that can be categorized.
3. **The three reports** — Balance Sheet, Profit & Loss, and Cash Flow statement are the reports Chris uses most.
4. Beyond that, it's a QuickBooks clone: it should grow the features any good accounting software has (see [roadmap.md](roadmap.md)).

## Non-negotiable foundation
Real **double-entry bookkeeping** under the hood — every transaction posts balanced debits and credits. The three reports are only trustworthy if the ledger is, so the posting engine is the heart of the app and the most heavily tested code in it.

## Hosting
Deployed on **Railway** (Chris's choice). v0 proves the ledger locally; deployment with access control is the milestone right after.
