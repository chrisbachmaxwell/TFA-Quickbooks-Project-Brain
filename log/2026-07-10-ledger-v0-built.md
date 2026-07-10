# 2026-07-10 — Ledger v0 built, adversarially reviewed, closed

One session ran the whole first loop: worker cycle 1 (build), architect review (falsification + fresh-context adversarial review), worker cycle 2 (fixes), architect close.

## Decisions made
- D-007: transfer matching deferred to M4; one-sided categorization convention documented in concepts/.
- D-008: ledger invariants get DB-level backstops (CHECK constraints, case-insensitive unique names), not just code checks.
- Goal 002 (Railway deploy + login + backups) drafted as the next active goal.

## Mistakes caught (the review earned its keep)
1. **Critical:** concurrent categorization (double-click / two tabs) posted two balanced entries for one bank transaction — silent book inflation that the balance-sheet ✓ can't see, and v0 has no delete to repair it. Fixed with a guarded `updateMany` (loser's transaction rolls back); reproduced first, then locked in by `e2e/integrity.spec.ts`, which fails against the pre-fix code.
2. Decimal-comma amounts ("12,34") imported 100x too large. Now rejected loudly.
3. Zero-amount statement rows imported but could never be categorized — permanent uncategorized-list jam. Now ignored at import with a visible count.
4. Impossible report dates (2026-99-99) rendered an empty balance sheet with a green "balanced ✓". Now an error banner.
5. Transfers double-count if both sides are categorized — deferred by design (D-007), documented as a concepts/ lesson.
6. Lesser: CSV space-before-quote, P2025 on stale account ids, case-sensitive duplicate account names.

## Patterns confirmed
- Gate falsification is worth the minutes: both sabotages (balance check removed; dedupe hash salted) were caught by exactly the intended test.
- The reviewer ran as a fresh agent context but on the **same model** as the worker (no second model available in this environment) — a deviation from the architect page's preference. It still found a critical bug; a different-model review remains preferred when available.
- Clean-checkout gates (fresh clone, `npm ci`, empty database) caught nothing extra this time but is cheap insurance; keep it in the close-out ritual.
- Reviewer false-alarm worth remembering: it briefly saw the worker's in-flight falsification sabotage (`Math.random()` in the dedupe hash) and correctly cleared it against the git blob. Don't run falsification while a reviewer reads the working tree.

## Commits pushed (code repo, branch `claude/project-factory-setup-rz0utl`)
- `9649ab5` — Ledger v0: chart of accounts, CSV import, categorization, balance sheet & P&L (33 unit + 15 e2e)
- `c5f0401` — review fixes + integrity migration (35 unit + 22 e2e)

Brain updated to match: goal 001 DONE, goal 002 PLANNED, status/roadmap current.
