# Spore

**One workspace. Every decision.**

Notes, meetings, and decisions — connected. A block-based workspace where context stays where it belongs.

[![Next.js](https://img.shields.io/badge/Next.js-16-black?logo=next.js)](https://nextjs.org/)
[![React](https://img.shields.io/badge/React-19-61DAFB?logo=react)](https://react.dev/)
[![Supabase](https://img.shields.io/badge/Supabase-Backend-3ECF8E?logo=supabase)](https://supabase.com/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-4-38B2AC?logo=tailwind-css)](https://tailwindcss.com/)

---

## Tags

`nextjs` `react` `supabase` `typescript` `tailwind` `workspace` `notes` `meetings` `documents` `collaboration` `block-editor` `real-time` `authentication` `oauth`

---

## Features

- **Block-based editor** — Text, code, tables, callouts, equations, and embedded media in one canvas. Structure appears as you write.
- **Meetings & decisions** — Schedule meetings, attach notes to events, and link action items to pages. Context stays with the call.
- **Workspaces** — One workspace per user (or team). Granular permissions and real-time sync so everyone stays on the same version.
- **Authentication** — Email/password sign up and sign in, plus Google and Microsoft OAuth. Optional email confirmation.
- **Inbox, calendar, sign** — Inbox view, calendar for events, and PDF signing flows integrated into the workspace.
- **Settings** — Profile, account, workspace, members, billing, notifications, and integrations (e.g. Google/Microsoft).

---

## Tech stack

| Layer        | Stack |
|-------------|--------|
| Framework   | Next.js 16 (App Router, Turbopack) |
| UI          | React 19, Tailwind CSS 4 |
| Backend     | Supabase (Postgres, Auth, Realtime, Storage) |
| State       | Zustand (client), Server Actions (mutations) |
| Editor      | Custom block editor (slash commands, drag-and-drop) |
| PDF         | pdf-lib, pdfjs-dist |

---

## Prerequisites

- **Node.js** 20+
- **npm** (or yarn/pnpm)
- **Supabase** account — [create a project](https://supabase.com/dashboard) and get URL + anon key (and service role key for seeding).

---

## Getting started

### 1. Clone and install

```bash
git clone https://github.com/kabir2004/spore.git
cd spore
npm install
```

### 2. Environment variables

Create `.env.local` in the project root:

```env
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
```

Optional (for seeding demo accounts and server-side admin):

```env
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
NEXT_PUBLIC_SITE_URL=http://localhost:3000
```

Get **Project URL** and **anon** (and **service_role**) keys from [Supabase Dashboard → Project Settings → API](https://supabase.com/dashboard/project/_/settings/api).

### 3. Database setup

Apply the schema and (optionally) seed data:

- **Option A — SQL Editor**  
  In [Supabase SQL Editor](https://supabase.com/dashboard/project/_/sql/new), run the contents of `supabase/seed.sql`.  
  Then run each file in `supabase/migrations/` in order (001 → 010) if you use migrations.

- **Option B — CLI**  
  `npx supabase login`, then `npx supabase link --project-ref <your-ref>`, then `npm run db:push`.

Enable **Realtime** for the `blocks` table: [Database → Replication](https://supabase.com/dashboard/project/_/database/replication) → enable **blocks**.

See [supabase/README.md](supabase/README.md) and [docs/seed-accounts.md](docs/seed-accounts.md) for details.

### 4. Run the app

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) (or the port shown in the terminal).  
Sign up at [http://localhost:3000/signup](http://localhost:3000/signup) or sign in at [http://localhost:3000/login](http://localhost:3000/login).

---

## Scripts

| Command | Description |
|--------|-------------|
| `npm run dev` | Start Next.js dev server (Turbopack) |
| `npm run build` | Production build |
| `npm run start` | Run production server |
| `npm run lint` | Run ESLint |
| `npm run db:push` | Push Supabase migrations (requires CLI + link) |
| `npm run db:migrate-010` | Run migration 010 via script (see script for env) |
| `npm run db:seed` | Seed DB via Management API (requires `SUPABASE_ACCESS_TOKEN`) |
| `npm run db:seed-accounts` | Create demo accounts (admin/user/test) — requires `SUPABASE_SERVICE_ROLE_KEY` |
| `npm run db:seed-demo` | Seed demo content — requires anon key |

---

## Project structure

```
spore/
├── app/                    # Next.js App Router
│   ├── (auth)/             # Login, signup, callback (auth group)
│   ├── (workspace)/        # Workspace UI: sidebar, pages, settings, inbox, etc.
│   ├── api/                # API routes (e.g. OAuth callbacks)
│   ├── auth/               # Auth confirm, layout
│   ├── globals.css
│   ├── layout.tsx          # Root layout, fonts, theme
│   └── page.tsx            # Landing page
├── components/             # React components
│   ├── auth/               # Auth inputs, alerts, social buttons
│   ├── editor/             # Block editor, slash menu, selection toolbar
│   ├── shared/             # Button, Avatar, AppLogo, CommandPalette, etc.
│   ├── sidebar/            # Sidebar nav, pages, header
│   ├── sign/               # PDF view, canvas, signature modal
│   ├── workspace/          # HomePage, MeetingsView, PageTransition
│   └── ...
├── lib/
│   ├── actions/            # Server Actions (auth, blocks, meetings, settings, etc.)
│   ├── context/            # React context (workspace, theme, document select-all)
│   ├── supabase/           # createClient (server/browser), service-role, types
│   ├── sync/               # useWorkspaceSync (realtime + store hydration)
│   ├── store/               # Zustand workspace store
│   ├── types/               # block, meeting, calendarEvent, sign, settings
│   └── utils/               # sanitize, cn, etc.
├── supabase/
│   ├── migrations/         # SQL migrations (001–010)
│   ├── seed.sql            # Base schema + seed (if used)
│   └── README.md           # Supabase setup
├── docs/                   # Additional documentation
│   ├── seed-accounts.md
│   ├── email-confirmation-setup.md
│   └── deployment.md
├── scripts/                # Seed and migration scripts (Node)
└── middleware.ts          # Auth refresh, protected routes
```

---

## Documentation

| Doc | Description |
|-----|-------------|
| [supabase/README.md](supabase/README.md) | Supabase credentials, schema, RLS, Realtime |
| [docs/seed-accounts.md](docs/seed-accounts.md) | Create admin/user/test accounts |
| [docs/email-confirmation-setup.md](docs/email-confirmation-setup.md) | Email confirmation and custom templates |
| [docs/deployment.md](docs/deployment.md) | Deploy to Vercel (env, redirect URLs) |

---

## Deployment

1. Set environment variables on your host (e.g. Vercel):
   - `NEXT_PUBLIC_SUPABASE_URL`
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - Optional: `NEXT_PUBLIC_SITE_URL` (e.g. `https://your-app.vercel.app`)

2. In Supabase → **Authentication → URL Configuration**:
   - Set **Site URL** to your production URL.
   - Add **Redirect URLs** (e.g. `https://your-app.vercel.app/auth/callback`, `https://your-app.vercel.app/**`).

3. Deploy (e.g. `vercel` or connect the repo to Vercel). See [docs/deployment.md](docs/deployment.md) for details.

---

## Troubleshooting

### "Invalid email or password" on deployed app

- Ensure the deployed app uses the **same** Supabase project (same `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY`) as the one where users exist.
- If you use seed accounts (`npm run db:seed-accounts`), run that against the **same** project and set `SUPABASE_SERVICE_ROLE_KEY` in your deploy env only if you run seed from CI; never expose the service role key to the browser.
- If **Confirm email** is enabled in Supabase, users must confirm before signing in; check spam/promotions for the confirmation email.
- Add your deployed URL to Supabase **Redirect URLs** and set **Site URL** so OAuth and email links point to the right domain.

### Port 3000 in use

Next.js will use the next available port (e.g. 3001). Check the terminal for the actual URL.

---

## Repository

- **GitHub:** [github.com/kabir2004/spore](https://github.com/kabir2004/spore)

---

## License

Private. All rights reserved.
