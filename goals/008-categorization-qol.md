# Goal 008 — Categorization quality of life: suggestions, bulk, starter accounts

**Status:** PLANNED
**Milestone:** part of M4 (smarter import), pulled forward
**Stop clause:** max 6 worker cycles, or 2 no-progress cycles → BLOCKED with reasons.

## Demo (what "works" looks like)
The second "Dividend - Acme Holdings" row arrives pre-selected to Dividend Income with a "suggested" hint — one click. Ten similar rows can be checked and categorized in one action. A brand-new book offers to install a sensible starter chart of accounts for a holding company in one click.

## Done when
- [ ] A review row whose description was categorized before gets that account pre-selected and visibly marked as suggested; unseen descriptions still show "Pick an account…" (verified by: Playwright `e2e/qol.spec.ts`)
- [ ] Rows can be selected with checkboxes and categorized to one account in a single submit; already-categorized or conflicting rows are skipped with a visible count (verified by: Playwright `e2e/qol.spec.ts`)
- [ ] An empty chart of accounts offers "Add starter accounts" which creates a holding-company starter set (cash, investments, liability, equity, income and expense accounts) exactly once — the button is gone once accounts exist (verified by: Playwright `e2e/qol.spec.ts`)
- [ ] Suggestion mapping is pure and unit-tested (last-used account per normalized description) (verified by: `npm test` — `suggestions.spec.ts`)
- [ ] All gates green (verified by: `npm run gates`)

## Waiting on Chris
- (nothing)

## Out of scope
- User-defined rule editor (regex/conditions) · ML anything

## Iteration log
- 2026-07-10 architect: drafted for the long autonomous run.
