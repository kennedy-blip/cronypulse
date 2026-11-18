# CronPulse

CronPulse is a Vite + React + TypeScript cron dashboard with Vercel Serverless API routes.

## Development

```bash
npm install
npm run dev
```

The Vite-only dev server uses the dashboard's demo data. To run API routes locally, install the Vercel CLI and use `vercel dev`.

## API

- `GET /api/crons` — list jobs and recent events
- `POST /api/crons` — create a job with `name`, `expression`, `endpoint`, and optional `timeout`
- `PATCH /api/crons` — `{ "id": "…", "action": "pause|resume|trigger" }`
- `POST /api/heartbeat` — record `{ "id": "…", "status": "success|failed", "duration": 250 }`
- `GET /api/heartbeat/:id` — job uptime and heartbeat history

## Deployment

Import this repository into Vercel. The framework is Vite; the root directory is the repository root and the build command is `npm run build`. No environment variables are required for the demo.

## Important runtime note

The included scheduler store is in-memory and intended as a functional prototype. Vercel serverless instances can restart and do not run continuously, so state is not durable and cron expressions are not automatically executed by this app. For production scheduling, add durable storage (such as Postgres/Redis) and configure Vercel Cron or an external scheduler to invoke a protected worker endpoint. Secure that endpoint with an authentication secret before exposing it publicly.
