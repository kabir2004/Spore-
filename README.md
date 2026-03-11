<p align="center">
  <img src="https://img.shields.io/badge/Next.js-16-000?style=flat-square&logo=next.js" alt="Next.js" />
  <img src="https://img.shields.io/badge/React-19-61DAFB?style=flat-square&logo=react" alt="React" />
  <img src="https://img.shields.io/badge/Supabase-3ECF8E?style=flat-square&logo=supabase" alt="Supabase" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Tailwind-38B2AC?style=flat-square&logo=tailwind-css" alt="Tailwind" />
</p>

# Spore

**One workspace. Every decision.**

Spore is a modern workspace that unifies notes, meetings, email, and decisions in a single block-based canvas. Context stays attached to the work—no more scattered docs, lost threads, or action items that slip through the cracks.

---

## The product

### Workspace & editor

- **Block-based canvas** — Text, code, tables, callouts, equations, and embedded media in one place. Structure emerges as you write. Slash commands, drag-and-drop, and real-time sync.
- **Workspaces** — Per-user or team workspaces with granular permissions. Everyone stays on the same version.

### Email & inbox

- **Gmail** — Connect your Gmail account to read and send emails directly from Spore. Search, star, archive, and reply without leaving the workspace.
- **Outlook** — Connect Microsoft Outlook (Outlook.com / Microsoft 365) to bring your Outlook mail into the same inbox. Read, send, and manage messages alongside your notes and meetings.

One unified inbox in Spore; connect either Gmail or Outlook (or both, per workspace) and keep communication next to the work it belongs to.

### Calendar & meetings

- **Google Calendar** — Sync events, create meetings, and see your schedule alongside Spore. Events and notes stay linked.
- **Outlook Calendar** — Sync Microsoft calendar events and manage availability from the workspace.
- **Meetings in context** — Schedule meetings, capture notes inside the event, and link action items directly to pages. When the call ends, nothing falls out of context.
- **Cal.com** — Connect your Cal.com booking page so teammates can schedule time with you.
- **Zoom** — Auto-generate Zoom links when creating meetings.

### Integrations & AI

- **Slack** — Send Spore notifications into your Slack channels.
- **AI models** — Connect Claude (Anthropic), OpenAI / ChatGPT, Google Gemini, or Groq to write, summarize, and reason inside your pages. API-key based; no OAuth required.

### Signing & more

- **PDF signing** — Upload PDFs, place signature fields, and collect signatures inside the workspace.
- **Auth** — Email/password sign up and sign in, plus **Google** and **Microsoft** OAuth. Optional email confirmation.
- **Settings** — Profile, account, workspace, members, billing, notifications, and integrations (Gmail, Outlook, calendars, Cal.com, Zoom, Slack, AI) all in one place.

---

## Why Spore

| | |
|---|---|
| **Unified canvas** | Notes, email, and meetings live in one workspace. Structure appears as you write. |
| **Email where you work** | Gmail and Outlook inside Spore—read, reply, and search without switching tabs. |
| **Meetings that stick** | Calendar sync (Google & Outlook), meeting notes, and action items linked to pages. |
| **Integrations** | Cal.com, Zoom, Slack, and AI (Claude, OpenAI, Gemini, Groq) connect in Settings. |
| **Production-ready** | Real-time sync, granular permissions, PDF signing, and full auth (email + Google + Microsoft). |

---

## Quick start

**Prerequisites:** Node.js 20+, npm, and a [Supabase](https://supabase.com/dashboard) project.

```bash
git clone https://github.com/kabir2004/Spore-.git
cd Spore-
npm install
```

Add `.env.local` in the project root:

```env
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
```

Run the schema (Supabase SQL Editor or CLI—see [supabase/README.md](supabase/README.md)), enable **Realtime** for the `blocks` table, then:

```bash
npm run dev
```

Open the URL shown in the terminal (e.g. `http://localhost:3000` or `3001`). Sign up at `/signup` or sign in at `/login`. Connect **Gmail** or **Outlook** from the Inbox or **Settings → Integrations** to try the unified inbox.

---

## Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start dev server (Turbopack) |
| `npm run build` | Production build |
| `npm run start` | Run production server |
| `npm run lint` | Run ESLint |
| `npm run db:push` | Push Supabase migrations (CLI required) |
| `npm run db:seed-accounts` | Create demo accounts (requires `SUPABASE_SERVICE_ROLE_KEY`) |
| `npm run db:seed-demo` | Seed demo content |

---

## Tech stack

- **Framework:** Next.js 16 (App Router, Turbopack)
- **UI:** React 19, Tailwind CSS 4
- **Backend:** Supabase (Postgres, Auth, Realtime, Storage)
- **State:** Zustand + Server Actions
- **Editor:** Custom block editor (slash commands, drag-and-drop)
- **PDF:** pdf-lib, pdfjs-dist

---

## Documentation

- [Supabase setup](supabase/README.md) — Credentials, schema, RLS, Realtime
- [Seed accounts](docs/seed-accounts.md) — Demo users (admin/user/test)
- [Email confirmation](docs/email-confirmation-setup.md) — Confirm signup flow
- [Deployment](docs/deployment.md) — Vercel, env vars, redirect URLs

---

## Deploying

1. Set `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`, and optionally `NEXT_PUBLIC_SITE_URL` in your host (e.g. Vercel).
2. In Supabase → **Authentication → URL Configuration**, set **Site URL** and add **Redirect URLs** for your production domain (e.g. `https://your-app.vercel.app/auth/callback`).
3. For **Gmail** and **Outlook** integrations, configure the corresponding OAuth apps (Google Cloud Console / Microsoft Azure) and set `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`, `MICROSOFT_CLIENT_ID`, `MICROSOFT_CLIENT_SECRET` (and redirect URIs) in your host. See [docs/deployment.md](docs/deployment.md) for details.

---

## Troubleshooting

- **"Invalid email or password" on deploy** — Use the same Supabase project and env vars as where users exist; add the deployed URL to Supabase Redirect URLs; if email confirmation is on, users must confirm before signing in.
- **Port in use** — Next.js will pick the next free port (e.g. 3001); use the URL printed in the terminal.

---

## Repository

**[github.com/kabir2004/Spore-](https://github.com/kabir2004/Spore-)**

---

*License: Private. All rights reserved.*
