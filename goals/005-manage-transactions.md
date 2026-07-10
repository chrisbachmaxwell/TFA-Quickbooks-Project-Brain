# Goal 005 — Manage transactions: undo, exclude, manual journal entries

**Status:** PLANNED
**Milestone:** part of M5 (the rest of a real accounting package), pulled forward
**Stop clause:** max 8 worker cycles, or 2 no-progress cycles → BLOCKED with reasons.

## Demo (what "works" looks like)
A miscategorized transaction can be undone and redone. A junk statement row (personal spend, bank artifact) can be excluded without polluting the books, and restored if that was wrong. Anything a statement can't express — accruals, corrections, opening balances — can be posted as a manual journal entry from a form that refuses to save unbalanced.

## Done when
- [ ] "Undo" on a categorized transaction deletes its journal entry atomically and returns the row to For review; the ledger afterwards holds no orphan lines (verified by: Playwright `e2e/manage.spec.ts` + DB assertion in the same spec)
- [ ] "Exclude" on a review row moves it to an Excluded section (never posted, not in reports); "Restore" brings it back (verified by: Playwright `e2e/manage.spec.ts`)
- [ ] Excluded rows still count as already-imported for dedupe — re-uploading the statement does not resurrect them (verified by: Playwright `e2e/manage.spec.ts`)
- [ ] `/journal` lists every journal entry (date, memo, lines, source: bank/manual) newest first (verified by: Playwright `e2e/journal.spec.ts`)
- [ ] A manual journal entry form (2+ lines, account + debit/credit each, live running totals) posts through the same validated engine; unbalanced submissions are rejected with the imbalance shown, and nothing is written (verified by: Playwright `e2e/journal.spec.ts`)
- [ ] Manual entries can be deleted; bank-linked entries cannot be deleted from `/journal` (only undone from the review screen) (verified by: Playwright `e2e/journal.spec.ts`)
- [ ] All gates green (verified by: `npm run gates`)

## Waiting on Chris
- (nothing)

## Out of scope
- Editing entries in place (delete + re-create is v1) · attachments

## Iteration log
- 2026-07-10 architect: drafted for the long autonomous run.
