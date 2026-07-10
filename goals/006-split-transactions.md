# Goal 006 — Split categorization

**Status:** DONE (2026-07-10)
**Milestone:** part of M5, pulled forward
**Stop clause:** max 6 worker cycles, or 2 no-progress cycles → BLOCKED with reasons.

## Demo (what "works" looks like)
A single card payment that covers, say, insurance and office supplies can be split across both expense accounts from a Split screen; the review row shows "Split" in its category and the P&L shows each part in the right place.

## Done when
- [x] Each For-review row links to a Split screen listing the transaction and N split lines (account + amount); amounts must be positive integers cents summing exactly to the transaction amount, enforced server-side with the difference shown on error (verified by: Playwright `e2e/split.spec.ts`)
- [x] Submitting posts ONE balanced journal entry (bank line + one line per split) through the validated engine; the row lands in Categorized showing "Split (N)" (verified by: Playwright `e2e/split.spec.ts` + DB balance assertion)
- [x] Undo works on split transactions exactly like simple ones (verified by: Playwright `e2e/split.spec.ts`)
- [x] The P&L reflects the split parts in their separate accounts, matching hand-computed totals (verified by: Playwright `e2e/split.spec.ts`)
- [x] All gates green (verified by: `npm run gates`)

## Waiting on Chris
- (nothing)

## Out of scope
- Splitting manual journal entries (already multi-line by nature)

## Iteration log
- 2026-07-10 architect: drafted for the long autonomous run.
- 2026-07-10 worker (cycle 1): built as specced; gates 56 unit + 46 e2e green first run. Commit `5016d8c`.
