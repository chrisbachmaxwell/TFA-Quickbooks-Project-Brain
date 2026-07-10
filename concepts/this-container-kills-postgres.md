# The dev container silently kills Postgres between work bursts

Twice in one session, `npm run gates` failed at the e2e stage with Prisma `P1001: Can't reach database server` — after the same command had passed minutes earlier. The Postgres log showed no shutdown message: the postmaster was SIGKILLed by the environment (managed containers reap idle daemons), not crashed by anything we did.

**The habit:** in remote/managed dev environments, run `pg_isready -q || service postgresql start` before any gates run or e2e work. Don't debug the app when the database simply isn't running — check `pg_lsclusters` first. A P1001 right after a green run is almost never your code.
