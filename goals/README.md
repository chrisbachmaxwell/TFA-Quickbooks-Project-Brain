# goals/ — how goals work

## The loop rules

1. **One page per goal.** A goal that needs two pages is two goals.
2. **One active goal per repo** at a time. The worker works only the active goal.
3. **Every "Done when" item must be agent-verifiable** and must end with **"(verified by: \<exact command or test name\>)"**. An item that can't name its check **isn't ready to be worked** — the architect finishes specifying it first.
4. **Anything needing Chris's hands** (accounts, credentials, purchases, judgment calls) goes under **"Waiting on Chris"**, not in "Done when".
5. **Every goal has a stop clause**: a max cycle count, and 2 consecutive no-progress cycles → set Status: BLOCKED and write exactly why. Obey it literally.
6. **Status is one of:** PLANNED · IN PROGRESS · BLOCKED · DONE.
7. Boxes get checked only when their named check ran green. The architect adversarially re-verifies and unchecks (with dated reasons) anything that doesn't hold.
8. Per the verification ratchet ([../CLAUDE.md](../CLAUDE.md)): a goal may not close with weaker checking tools than it opened with.

## Goal-page template (copy everything below)

```markdown
# Goal NNN — <title>

**Status:** PLANNED
**Milestone:** <link to roadmap entry>
**Stop clause:** max <N> worker cycles, or 2 consecutive no-progress cycles →
set Status: BLOCKED and write exactly why below.

## Demo (what "works" looks like)
A user can <X> and see <Y>.

## Done when
- [ ] <agent-verifiable item> (verified by: <exact command or test name>)
- [ ] <agent-verifiable item> (verified by: <exact command or test name>)

## Waiting on Chris
- (nothing yet)

## Out of scope (goes to roadmap, not code)
- <item>

## Iteration log
- YYYY-MM-DD <role>: <what happened, gate results, commit hash>
```
