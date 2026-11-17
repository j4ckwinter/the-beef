# vitals on this Mac

vitals is Jack's self-hosted real-user monitoring: a browser beacon, a collector API on Postgres, alerts and a dashboard. It was built on 17–18 November 2026 as a portfolio project for the senior-engineering improvement plan in his Notion. Its checkout is `../vitals`, relative to this repository's root. This page describes the Mac.

The project owns its own facts. Read its [contributor instructions](../../vitals/AGENTS.md), [README](../../vitals/README.md), [runbook](../../vitals/docs/runbook.md) and [guide](../../vitals/docs/guide.md).

## The state of the checkout

Checked on 18 November 2026.

- It has no Git remote. Nothing has been pushed or deployed. The beacon is not on any live site.
- Jack said he likes his portfolio as it is. Adding the beacon to jackwinter.xyz deploys that site, so it needs his request. Measuring something else instead, such as the padel game, was also offered.

## What it uses on this Mac

- Docker through Colima. `compose.yaml` runs two containers:
  - `vitals-postgres-1` on `127.0.0.1:5433`, holding three databases. `vitals` is for development and has seeded demo data. `vitals_test` is wiped by `npm run test:postgres`, and `vitals_bench` is wiped by `npm run bench`.
  - `vitals-jaeger-1`, with its UI on `127.0.0.1:16686` and OTLP on `127.0.0.1:4317` and `4319`.
- `.env` in the checkout holds local-only settings, including a development dashboard password.
- Playwright's Chromium headless shell 1254 was downloaded to `~/Library/Caches/ms-playwright` for its end-to-end test. Deedspan uses the same Playwright version.
- The collector listens on `127.0.0.1:4318`, and the demo site on `localhost:4400`. Neither runs at login.
