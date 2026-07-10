# Brain rules — TFA-Quickbooks-Project-Brain

These rules bind every agent, in every tool, on every model, that touches this repo.
(`CLAUDE.md` and `AGENTS.md` are identical mirrors — if you edit one, make the same edit to the other.)

## The four laws of this brain

1. **One lesson per file.** A concepts/ page holds exactly one hard-won lesson. Don't bundle.
2. **Update, don't duplicate.** Before writing anything, check whether a page for it already exists. Improve that page; never create a second page saying almost the same thing.
3. **Delete what's wrong (and log the correction).** A wrong page is worse than no page. When the field contradicts a page, fix or delete the page immediately, and record the correction in your session's log/ note.
4. **Never touch raw/.** raw/ is append-only ground truth (logs, evidence, pastes). Agents may add files there; agents never edit or delete anything in it.

## Reading discipline

Reading is **pay-per-read**: context is expensive. Start at [INDEX.md](INDEX.md), follow links to exactly what your situation needs, and stop. Never sweep folders "to get oriented".

## Freshness

Volatile claims (versions, prices, external-service behavior, anything that rots) must carry a marker: **"(verify after: YYYY-MM)"**. When you read a claim past its date, verify it before relying on it, then update the marker.

## Every session ends the same way

Before you stop working — every time, no exceptions:

1. Write a **dated note in log/** (`log/YYYY-MM-DD-short-title.md`) covering: decisions made, mistakes caught, patterns confirmed, and the commit hashes you pushed.
2. Update [entities/project-status.md](entities/project-status.md) and [entities/roadmap.md](entities/roadmap.md) so they **match reality** — a status page that lags reality is a lie to the next agent.

## Sync

Single sync system: **git only**, with manual push checkpoints. Commit and push both repos (code first, then brain) at every checkpoint. No other sync mechanism, ever.

## THE VERIFICATION RATCHET

Every bug found in the field becomes an **automated check** — a test, a simulator behavior, or a gate — **before its fix counts as done**. No exceptions. The checking tools must end every goal stronger than they started it: if a goal closes and the gates can't catch one more class of mistake than they could when it opened, the goal isn't done.
