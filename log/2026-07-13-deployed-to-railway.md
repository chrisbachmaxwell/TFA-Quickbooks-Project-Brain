# 2026-07-13 — Deployed to Railway (goal 002 demo complete)

Chris supplied a Railway account token; setup ran entirely via the Railway CLI from the session container.

- Project **TFA-Books** · Postgres service · **tfa-books** app service created with `railway add --repo chrisbachmaxwell/TFA-Quickbooks --branch claude/project-factory-setup-rz0utl` → GitHub-linked, so **every push auto-deploys** (the thing the CLI supposedly couldn't do — `railway add --repo` does it).
- Variables: `DATABASE_URL=${{Postgres.DATABASE_URL}}` reference + generated `APP_PASSWORD`. Domain: <https://tfa-books-production.up.railway.app>.
- Verified live: unauthenticated routes 307 → /login; login page 200; app booting proves `prisma migrate deploy` ran (start command chains it before `next start`).
- Environment lesson: the Claude Code environment's network policy initially blocked backboard.railway.com (proxy CONNECT 403) — that policy is separate from claude.ai's chat-sandbox "Capabilities" toggles; Chris opened it and everything flowed.
- Security follow-ups for Chris: revoke the CLI token in Railway → Account → Tokens (it was pasted in chat); optionally rotate APP_PASSWORD in the tfa-books service Variables (also surfaced in chat).
- A `.railwayignore` was added to the code repo (belt-and-braces against uploading .env/backups on any future `railway up`).
