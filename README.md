# StrangerLoop

A mobile-friendly random text/video chat starter built with Express, Socket.IO and WebRTC.

## Features
- Random one-to-one matching with optional shared interests
- Live text messages with basic rate limiting
- WebRTC video/audio signaling; camera/mic permission is requested by the browser
- Report and leave controls
- Authenticated admin summary endpoint for active room metadata, reports, and temporary text-message review
- Clear privacy notice; no server-side video/audio recording

## Run locally
1. Install Node.js 20 or newer.
2. In this folder run `npm install`.
3. Copy `.env.example` to `.env` and set a strong `ADMIN_TOKEN`.
4. Run `npm start` and open `http://localhost:3000`.

For local testing across two browser windows, both should connect to the same running server.

## Admin endpoint
Request `GET /admin/summary` with header `x-admin-token: YOUR_SECRET`. Set `ADMIN_TOKEN` in your hosting provider's secret/environment settings. Do not put the secret in frontend code or commit it to GitHub. The endpoint returns active room metadata, recent reports, and recent text messages. Messages are held in memory only and disappear when the server restarts.

## Deployment
Deploy as a Node.js web service on a host that supports long-lived WebSocket connections and environment variables. Configure:
- Start command: `npm start`
- Environment variable: `ADMIN_TOKEN` (strong random value)
- HTTPS enabled
- Any platform-specific health check path: `/health`

Do not deploy this as a static-only GitHub Pages site: Socket.IO requires a running server. Free hosting plans and quotas change; verify current limits before choosing a provider.

## Important production hardening
This is a starter, not a fully audited public service. Before public launch, add a real moderation workflow, durable report handling, admin authentication with accounts/MFA rather than a shared token, bot protection/CAPTCHA, stronger IP and user rate limits, abuse escalation and retention policies, jurisdiction-specific legal review, and robust WebRTC TURN service configuration. A STUN-only connection may fail for users behind restrictive NATs; add a TURN provider for reliable video. Do not advertise guaranteed anonymity. Only permit adult users if you can enforce and legally support that policy.
