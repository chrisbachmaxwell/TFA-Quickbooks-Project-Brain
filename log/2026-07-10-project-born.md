# 2026-07-10 — Project born (factory session)

**What happened:** TFA-Quickbooks was created from Chris's project-factory prompt. Both repos scaffolded: code repo (README, .gitignore, agent instructions with aspirational gates) and this brain (full structure, seeded entities, goal 001 drafted).

**Decisions made:** D-001 through D-006 in [../entities/decisions.md](../entities/decisions.md) — stack (Next.js/TS/Prisma/Postgres for Railway), Postgres everywhere, integer-cent money, double-entry from day one, v0 local-only, CSV upload before bank feeds.

**Mistakes caught:** none yet — nothing built.

**Patterns confirmed:** n/a (first session).

**Open items:** goal 001 is PLANNED and ready for a worker. Chris declined the constraints question; privacy defaults were chosen conservatively (no real financial data until M2's login + deployment). A real bank CSV sample from Chris would improve the import fixture but isn't blocking.

**Commits:** initial commits on branch `claude/project-factory-setup-rz0utl` in both repos (hashes in git history; this is the first commit, so no prior hash to reference).
