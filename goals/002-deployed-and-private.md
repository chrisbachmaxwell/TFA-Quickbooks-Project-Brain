# Goal 002 — Deployed and private

**Status:** DONE (2026-07-10 — code side; Railway clicking waits on Chris)
**Milestone:** [M2 — Deployed and private](../entities/roadmap.md)
**Stop clause:** max 10 worker cycles, or 2 consecutive no-progress cycles →
set Status: BLOCKED and write exactly why below.

## Demo (what "works" looks like)
Chris opens the app's Railway URL on his phone, is asked to log in, logs in with the app password, and sees the same books the browser tests exercise — while a logged-out visitor sees nothing but the login page. The database survives a redeploy and has a restorable backup.

## Done when
- [x] Every page and server action except the login screen rejects unauthenticated visitors (redirect to /login), enforced by middleware, and logging in with the password from the `APP_PASSWORD` env var creates a session that survives a browser restart (cookie, httpOnly, secure) (verified by: Playwright `e2e/auth.spec.ts`)
- [x] Logging out ends the session; a logged-out user hitting any page is back at /login (verified by: Playwright `e2e/auth.spec.ts`)
- [x] Wrong password shows an error and never creates a session; login attempts are rate-limited (verified by: Playwright `e2e/auth.spec.ts`)
- [x] The full existing suite still passes with auth enabled — the e2e helpers log in once and reuse the session (verified by: `npm run gates`)
- [x] The repo contains a working Railway deployment config (start command runs `prisma migrate deploy` before `next start`; `PORT` respected; `DATABASE_URL` and `APP_PASSWORD` read from Railway env) and a `docs/deploy.md` with exact click-by-click Railway steps for a non-technical operator (verified by: `npm run gates` — config files lint/build; the doc's commands are copy-pasteable and referenced from README)
- [x] A backup/restore script exists: `npm run db:backup` writes a timestamped dump, `npm run db:restore <file>` restores it into an empty database, and a test proves a backup taken after posting entries restores to identical report totals (verified by: `e2e/backup-restore.spec.ts` or a Vitest integration test named `backup-restore`)

## Waiting on Chris
- Create the Railway project (app service + Postgres) and set `DATABASE_URL`, `APP_PASSWORD` env vars — `docs/deploy.md` (written by this goal) will walk through it click by click.
- Choose the app password (never commit it anywhere).
- After first deploy: confirm the demo above works from his phone, then tell the tester/architect.

## Out of scope (goes to roadmap, not code)
- Multi-user accounts, roles, OAuth (single shared password is M2's scope)
- Cash Flow statement (M3), bank feeds and transfer matching (M4)

## Iteration log
- 2026-07-10 architect: goal drafted at close of goal 001. Not started.
- 2026-07-10 worker (cycle 1): HMAC-cookie auth (middleware on every route, rate-limited login, logout in sidebar), Playwright auth.setup storage-state project, pg_dump/psql backup+restore scripts with an e2e gate proving a wiped ledger restores to identical totals, railway.json + docs/deploy.md click-by-click. Two real bugs shaken out on the way: the login rate-limit map moved to globalThis (bundler duplicates module state per chunk), and the rate-limit e2e loop needed a deterministic per-attempt sync (old error banner satisfied the assertion before the new submission landed). Gates: 42 unit + 32 e2e green. Commit `8782048`.
