# 2026-07-11 — The parity run: eight goals, two review rounds, done

One continuous autonomous session (authorized by Chris) executed goals 002 and 004-010, then a full adversarial review round. Suite grew from 42 unit + 26 e2e to **79 unit + 65 e2e**; clean-checkout gates green.

## Decisions made
- D-009 (invoicing parked) held; run spent effort on books-quality instead.
- Review fix set: matched-row categorization guard, unmatch escape hatch, global rate-limit cap, atomic import matching, cash-only dashboard tile.

## Mistakes caught
1. **Review round 2, CRITICAL**: matched transfer-mirror rows could still be categorized (stale tab, or transfer legs >3 days apart) — silently double-posting. Fixed + gated (direct-call rejection tests in e2e/transfers.spec.ts).
2. Rate limit keyed on client-controlled x-forwarded-for → bypassable by rotation. Fixed with a global failure cap (lib/rate-limit.ts, unit-tested).
3. **Process blunder (mine)**: falsified the matched-row fix BEFORE committing it — `git checkout` during restore silently wiped the fix; only re-running the spec caught it. Rule added to roles/architect.md: commit fixes before falsifying.
4. Latent dashboard bug found by goal 009: review count included excluded rows.
5. e2e traps documented along the way: Playwright hasText matches <select> option text (filter description cells exactly); await a DOM change after actions before goto(); uncontrolled selects keep DOM value across soft navigations (key-remount).

## Patterns confirmed
- One goal at a time with gates between each: 6 of 8 goals were green on the first full run; the two that weren't were test-synchronization issues, not app bugs.
- Fresh-context adversarial review keeps earning its keep: both rounds found a critical, silent, balanced-books corruption bug that no gate covered.
- Falsification sample this round: transfer matcher, cash-flow classifier, split sum check, auth middleware, matched-row guard — all five gates went red on sabotage.

## Commits pushed (code repo)
8782048 auth+backups+deploy · e9ce429 cash flow · 54b1e8c manage txns · 5016d8c splits · dcf9485 registers/TB/GL · 50e4632 QoL · 4d4c4a4 transfers · 4cec6ef exports/comparison · 066ab04 review fixes
