# Goal 012 — QuickBooks-style chart-of-accounts templates & suggested accounts

**Status:** DONE (2026-07-13)
**Milestone:** requested by Chris 2026-07-13: "I don't want to create all the charts in the chart of accounts, quickbooks has suggested and standard ones. can you make that as well"
**Stop clause:** max 6 worker cycles, or 2 no-progress cycles → BLOCKED with reasons.

## Demo (what "works" looks like)
A new book offers a choice of standard charts — Holding & investment company, General small business, Rental property — and one click installs the whole thing. On an existing book, a "Suggested accounts" section lists the standard accounts you don't have yet; add them one at a time or all at once, QuickBooks-style.

## Done when
- [x] A pure template library ships ≥3 standard charts (holding/investment, general small business, rental property), each with typed accounts, cash flags on bank accounts, and case-insensitively unique names; a pure `missingAccounts()` computes what a book lacks (verified by: `npm test` — `coa-templates.spec.ts`)
- [x] An empty chart of accounts offers a template picker; installing creates every account with correct types and cash flags (verified by: Playwright `e2e/coa-templates.spec.ts`)
- [x] A "Suggested accounts" section on the accounts page shows, per selected template, only the accounts missing (case-insensitive); individual Add and "Add all missing" both work and the section empties out (verified by: Playwright `e2e/coa-templates.spec.ts`)
- [x] All gates green including reworked qol.spec (the old 17-account starter is replaced by the holding template) (verified by: `npm run gates`)
- [x] Deployed; production accounts page shows the picker (verified by: curl/live check in iteration log)

## Waiting on Chris
- (nothing)

## Out of scope
- Account numbers/codes · sub-accounts/hierarchy · industry-specific tax mappings

## Iteration log
- 2026-07-13 architect: drafted from Chris's mid-run request.
- 2026-07-13 worker: built and deployed. Three templates (holding 29, small business 34, rental 25 accounts); suggested-accounts section with per-account Add and add-all; qol.spec reworked to the holding template. Gates 91 unit + 75 e2e green. Deployment SUCCESS on Railway; app serving after `prisma migrate deploy` proves migrations applied. One e2e race fixed (await the action's redirect before navigating — same lesson as goal 005, now bitten twice).
