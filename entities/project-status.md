# Project status

**As of 2026-07-11 — THE PARITY RUN IS COMPLETE.** TFA Books now covers the core of a real accounting package, all of it gated: **79 unit + 65 Playwright browser tests** via `npm run gates`, green from a clean checkout.

## What works
- **Books**: chart of accounts (types, cash flag, starter set, registers with running balances), bank-statement CSV import (dedupe, zero-row handling, row-numbered errors), categorization (suggestions from payee memory, bulk, splits across accounts, undo, exclude/restore), manual journal entries (live-balancing form), transfer matching between own accounts (auto-match at categorize- and import-time, unmatch escape hatch, double-post guards).
- **Reports**: Balance Sheet, P&L (with previous-period comparison), Cash Flow (direct method, reconciles with the balance sheet), Trial Balance, General Ledger, reports hub, CSV export for all statements, date presets, print styles.
- **App**: Wave-style shell (sidebar, dashboard with KPIs + monthly chart), single-password login (HMAC cookie, middleware on every route, spoof-resistant rate limiting), pg_dump backup/restore with a restore-proving test, Railway deploy config + click-by-click docs/deploy.md.

## Reviews
Two adversarial review rounds (fresh-context agent, same model — no second model available). Round 2 found 1 critical (matched transfer-mirror rows could be categorized → silent double-post) + 4 lesser; all five fixed with ratchet tests in the final commit. Gate falsification performed on 5 gates across the run — every one went red on sabotage.

## Where things stand
- **Goals 001–010: ALL DONE.** Each goal page carries its iteration log and commit hashes.
- **Deployment: waiting on Chris** — the only remaining item from goal 002. docs/deploy.md in the code repo walks through Railway click by click (~10 min).
- **Deliberately not built**: invoicing/AR (D-009 — likely irrelevant for a holding company; ask Chris), multi-entity (M6), bank feeds (M4 evaluation pending).
- Everything on branch `claude/project-factory-setup-rz0utl` (GitHub default).

## Next action
Chris deploys via docs/deploy.md and starts putting TFA's real books in. Next natural goals when work resumes: multi-entity (M6) or bank-feed evaluation (M4) — architect should interview Chris first.
