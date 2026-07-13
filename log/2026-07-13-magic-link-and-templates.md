# 2026-07-13 — Passwordless login + CoA templates (goals 011, 012), deployed

Chris asked for email-link login with an allowlist (seed chrism@pictureline.com) and QuickBooks-style standard charts of accounts. Both shipped and deployed same-day.

## Decisions
- Magic links via **Resend** behind a pure module boundary; no key → links print to the server log, which doubles as lockout recovery (read the link in Railway Logs).
- Sessions are stateless HMAC cookies over SESSION_SECRET (edge-verifiable, no DB in middleware); allowlist re-checked when a link is redeemed, so removing a user kills outstanding links; cookies age out ≤30d.
- Rate limiting keyed on ip+email pair (per-IP alone would let one shared IP starve the e2e suite — and NAT'd households).
- Templates are pure data (3 charts, 20+ accounts each); "suggested accounts" = template minus existing names, case-insensitive.

## Mistakes caught
- Nested <form> generated in the suggested-accounts card (browsers silently drop the inner form) — caught on render review before tests.
- Same e2e race as goal 005 bit again: click → goto cancels the in-flight server action. Rule of thumb now twice-earned: after any action click, await its redirect/DOM effect before navigating.

## Gates
91 unit + 75 Playwright green; falsified allowlist check (e2e caught) and cookie signature verification (unit caught), fixes committed before falsifying per the new architect rule. Deployed: SESSION_SECRET set / APP_PASSWORD removed via CLI; deployment SUCCESS; production on the email login.
