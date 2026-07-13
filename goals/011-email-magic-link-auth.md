# Goal 011 — Passwordless email login with an authorized-user allowlist

**Status:** DONE (2026-07-13)
**Milestone:** requested by Chris 2026-07-13: "change the login for the app to not have a password but use a service that sends an email to login and only authorized users can login. add chrism@pictureline.com as a user."
**Stop clause:** max 8 worker cycles, or 2 no-progress cycles → BLOCKED with reasons.

## Demo (what "works" looks like)
Chris opens the app, types chrism@pictureline.com, clicks "Email me a sign-in link", gets an email, clicks the link, and he's in — no password anywhere. Anyone else typing their email sees the same neutral message but no link is ever created. A Users page lets Chris add or remove authorized emails.

## Done when
- [x] The login screen takes only an email; requesting a link for an authorized email creates a single-use token (hashed at rest, 15-minute expiry) and sends it; an unauthorized email shows the SAME neutral message and creates nothing (no user enumeration) (verified by: Playwright `e2e/auth.spec.ts` + DB assertions)
- [x] Visiting the emailed link signs the user in with a signed session cookie (HMAC over email+expiry with `SESSION_SECRET`, httpOnly, 30 days); the token is consumed — a second visit fails; expired and garbage tokens fail (verified by: Playwright `e2e/auth.spec.ts`)
- [x] Every page and route except /login and /login/verify rejects visitors without a valid signed cookie; tampered cookies are rejected (verified by: Playwright `e2e/auth.spec.ts`)
- [x] Email delivery goes through Resend when `RESEND_API_KEY` is set; otherwise the link is printed to the server log (dev mode and lockout-recovery via Railway logs) — the sender is a pure module boundary (verified by: unit test `magic-link.spec.ts` for token/cookie primitives; e2e drives the log-mode flow end to end)
- [x] Link requests are rate-limited per email+IP with the existing limiter (verified by: Playwright `e2e/auth.spec.ts`)
- [x] A Users page (inside the app) lists authorized emails and can add/remove them; removing the last user is refused; chrism@pictureline.com is seeded by migration (verified by: Playwright `e2e/users.spec.ts`)
- [x] APP_PASSWORD is fully retired from code, env examples, docs, and Railway; the whole suite runs on the new auth (verified by: `npm run gates` + `git grep APP_PASSWORD` returning only historical brain/log references)
- [x] Deployed to Railway with `SESSION_SECRET` set; live URL verified: protected routes redirect, login page renders email form (verified by: curl checks against production, recorded in the iteration log)

## Waiting on Chris
- A **Resend API key** (resend.com — free tier). Until it's set, sign-in links appear in Railway service logs instead of email.
- Ideally: verify a sending domain in Resend (otherwise Resend's test mode limits recipients).

## Out of scope
- OAuth/Google login · roles/permissions (all authorized users are equal) · session revocation list (removal takes effect for new logins; existing cookies age out in ≤30 days)

## Iteration log
- 2026-07-13 architect: drafted from Chris's request.
- 2026-07-13 worker: built and deployed. Gates 86 unit + 71 e2e green first run; falsified the allowlist check (e2e caught it) and cookie verification (unit caught it) — fix committed BEFORE falsifying this time. SESSION_SECRET set on Railway via CLI, APP_PASSWORD variable removed, production verified on the new login (307 redirects, email form live). RESEND_API_KEY still pending from Chris — until then sign-in links print to Railway service logs.
