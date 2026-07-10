# Goal 009 — Transfer matching between own accounts

**Status:** PLANNED
**Milestone:** [M4](../entities/roadmap.md) — retires the D-007 one-sided convention
**Stop clause:** max 6 worker cycles, or 2 no-progress cycles → BLOCKED with reasons.

## Demo (what "works" looks like)
Chris moves $5,000 from Checking to Savings. Both statements get imported. He categorizes the Checking row as a transfer to Savings — and the Savings-side mirror row is automatically matched and cleared from review. Both registers are right, nothing is double-counted, and the trial balance still sums to zero.

## Done when
- [ ] The category picker offers other cash accounts under a "Transfer" group; choosing one posts the balanced transfer entry (credit source, debit destination) (verified by: Playwright `e2e/transfers.spec.ts`)
- [ ] After posting, an uncategorized mirror row on the destination account (opposite amount, date within 3 days) is auto-matched: marked as matched-transfer (not posted, out of review, visibly labeled), linked to the same entry (verified by: Playwright `e2e/transfers.spec.ts`)
- [ ] If no mirror exists yet, importing the destination statement later auto-matches it at import time (verified by: Playwright `e2e/transfers.spec.ts`)
- [ ] Undoing the transfer un-matches the mirror row (back to review) as well (verified by: Playwright `e2e/transfers.spec.ts`)
- [ ] With both statements imported and the transfer categorized once, both account balances are correct and the trial balance is zero (verified by: Playwright `e2e/transfers.spec.ts` DB assertions)
- [ ] The matching logic (candidate selection: amount, account, date window, closest-date tie-break) is pure and unit-tested (verified by: `npm test` — `transfer-match.spec.ts`)
- [ ] [../concepts/transfers-double-count.md](../concepts/transfers-double-count.md) is rewritten for the new behavior and D-007 superseded in decisions.md (verified by: the pages themselves, checked in architect review)
- [ ] All gates green (verified by: `npm run gates`)

## Waiting on Chris
- (nothing)

## Out of scope
- Cross-currency transfers · fuzzy amount matching (fees) — parking lot

## Iteration log
- 2026-07-10 architect: drafted for the long autonomous run.
