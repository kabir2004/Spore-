<p align="center">
  <img src="https://img.shields.io/badge/Next.js-16-000?style=flat-square&logo=next.js" alt="Next.js" />
  <img src="https://img.shields.io/badge/React-19-61DAFB?style=flat-square&logo=react" alt="React" />
  <img src="https://img.shields.io/badge/Supabase-3ECF8E?style=flat-square&logo=supabase" alt="Supabase" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Tailwind-38B2AC?style=flat-square&logo=tailwind-css" alt="Tailwind" />
</p>

# Spore

**One workspace. Every decision.**

Spore is a modern workspace that unifies notes, meetings, and decisions in a single block-based canvas. Context stays attached to the work—no more scattered docs or lost action items.

---

## Why Spore

| | |
|---|---|
| **Unified canvas** | One place for text, code, tables, callouts, and media. Structure emerges as you write. |
| **Meetings that stick** | Schedule events, capture notes in-context, and link outcomes directly to pages. |
| **Workspaces & sync** | Per-user or team workspaces with real-time sync and granular permissions. |
| **Ready for production** | Auth (email + Google/Microsoft), inbox, calendar, PDF signing, and full settings. |

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

Open the URL shown in the terminal (e.g. `http://localhost:3000` or `3001`). Sign up at `/signup` or sign in at `/login`.

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
3. Deploy; see [docs/deployment.md](docs/deployment.md) for details.

---

## Troubleshooting

- **"Invalid email or password" on deploy** — Use the same Supabase project and env vars as where users exist; add the deployed URL to Supabase Redirect URLs; if email confirmation is on, users must confirm before signing in.
- **Port in use** — Next.js will pick the next free port (e.g. 3001); use the URL printed in the terminal.

---

## Repository

**[github.com/kabir2004/Spore-](https://github.com/kabir2004/Spore-)**

---

*License: Private. All rights reserved.*
