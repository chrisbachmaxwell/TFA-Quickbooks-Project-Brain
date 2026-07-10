# Goal 005 — Manage transactions: undo, exclude, manual journal entries

**Status:** DONE (2026-07-10)
**Milestone:** part of M5 (the rest of a real accounting package), pulled forward
**Stop clause:** max 8 worker cycles, or 2 no-progress cycles → BLOCKED with reasons.

## Demo (what "works" looks like)
A miscategorized transaction can be undone and redone. A junk statement row (personal spend, bank artifact) can be excluded without polluting the books, and restored if that was wrong. Anything a statement can't express — accruals, corrections, opening balances — can be posted as a manual journal entry from a form that refuses to save unbalanced.

## Done when
- [x] "Undo" on a categorized transaction deletes its journal entry atomically and returns the row to For review; the ledger afterwards holds no orphan lines (verified by: Playwright `e2e/manage.spec.ts` + DB assertion in the same spec)
- [x] "Exclude" on a review row moves it to an Excluded section (never posted, not in reports); "Restore" brings it back (verified by: Playwright `e2e/manage.spec.ts`)
- [x] Excluded rows still count as already-imported for dedupe — re-uploading the statement does not resurrect them (verified by: Playwright `e2e/manage.spec.ts`)
- [x] `/journal` lists every journal entry (date, memo, lines, source: bank/manual) newest first (verified by: Playwright `e2e/journal.spec.ts`)
- [x] A manual journal entry form (2+ lines, account + debit/credit each, live running totals) posts through the same validated engine; unbalanced submissions are rejected with the imbalance shown, and nothing is written (verified by: Playwright `e2e/journal.spec.ts`)
- [x] Manual entries can be deleted; bank-linked entries cannot be deleted from `/journal` (only undone from the review screen) (verified by: Playwright `e2e/journal.spec.ts`)
- [x] All gates green (verified by: `npm run gates`)

## Waiting on Chris
- (nothing)

## Out of scope
- Editing entries in place (delete + re-create is v1) · attachments

## Iteration log
- 2026-07-10 architect: drafted for the long autonomous run.
- 2026-07-10 worker (cycle 1): built as specced. Two e2e traps documented for posterity: Playwright hasText is case-insensitive substring over the WHOLE row — including <select> option text, so every review row 'contains' every account name (filter on the description cell with exact:true instead); and a click that triggers a server action must be awaited via a DOM state change before goto(), or the navigation cancels the action. Gates 52 unit + 42 e2e green. Commit `54b1e8c`.
