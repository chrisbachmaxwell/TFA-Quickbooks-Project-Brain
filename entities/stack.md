# Stack

Chosen by the factory on 2026-07-10 ("you choose, we will be hosting it on Railway" — Chris). Reasons in [decisions.md](decisions.md).

| Layer | Choice | Notes |
|---|---|---|
| Framework | **Next.js (App Router) + TypeScript** | One codebase for UI and API; deploys cleanly to Railway. (verify after: 2026-12) |
| Database | **PostgreSQL** | Railway managed Postgres in production; local dev/tests run against a local or Docker Postgres. (verify after: 2026-12) |
| ORM | **Prisma** | Schema + migrations live in the code repo. |
| Unit tests | **Vitest** | Posting engine and report math live here. |
| Browser tests | **Playwright** | Clicks the app like a user — the only proof a UI claim accepts. |
| Hosting | **Railway** | Not set up yet; milestone M2. |

## Conventions
- **Money is integer cents** (no floats, ever). Display formatting happens at the edge.
- Every transaction posts **balanced debits and credits**; the database schema must make an unbalanced posting unrepresentable or reject it.
- Account types: Asset, Liability, Equity, Income, Expense.

## How to run (updates as the code repo grows)
Nothing is built yet. The first goal ([../goals/001-ledger-v0.md](../goals/001-ledger-v0.md)) creates the app skeleton and the runnable gates. Once it does, the commands live in the code repo's `AGENTS.md` under "Build & verify" — that file is the single source of truth for gates; this page only points at it.
