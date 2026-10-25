# Talkz Cloud — free-first community chat

Talkz is an original Discord-inspired community chat project designed to run on Node.js and PostgreSQL. This build is intended for low-cost/free-tier hosting, but free providers may sleep, impose quotas, or change their plans.

## Current functionality

- Account registration and login with bcrypt password hashing and PostgreSQL-backed sessions
- Persistent servers, text channels, members, and messages
- Real-time text messages through Socket.IO
- Server invites with expiry, use limits, revocation, and authenticated joining
- Responsive mobile layout with channel drawer
- Message editing (author only), message deletion (author or moderator), emoji reactions, moderator pin/unpin, and channel message search
- Health endpoint at `/api/health`

## Not implemented yet

This is not feature-equivalent to Discord. Direct-message UI, friend requests, image/file uploads, video/voice calls, screen sharing, advanced permission overrides, bot ecosystem, push notifications, events, and full moderation dashboards still require separate implementation and testing. Voice/video may be possible with browser WebRTC, but reliable calls across restrictive networks can require TURN infrastructure that may not be free.

## Run locally

1. Install Node.js 20 or newer and PostgreSQL.
2. Copy `.env.example` to `.env` and fill in `DATABASE_URL` and `SESSION_SECRET`.
3. Run `npm install` then `npm start`.
4. Open `http://localhost:3000`.

## Render deployment

Keep the existing PostgreSQL database and environment variables. Required environment variables:

- `DATABASE_URL`: PostgreSQL connection string
- `SESSION_SECRET`: long random secret
- `TRUST_PROXY=true`: set when running behind Render's proxy so secure session cookies work

Set build command to `npm install` (or leave Render's detected package manager command if it works) and start command to `npm start`. The app creates/updates its tables on startup. Back up the database before deploying any new version.

## Security notes

Use HTTPS in production, keep secrets out of Git, and take a database backup before updates. Review the code and test permissions before opening a public community. This is a starter project, not a security-audited production service.
