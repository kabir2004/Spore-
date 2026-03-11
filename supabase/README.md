# Spore – Supabase setup

## Credentials

Create a [Supabase project](https://supabase.com/dashboard) and add these to `.env.local`:

- **Project URL** → `NEXT_PUBLIC_SUPABASE_URL` (e.g. `https://xxxxxxxx.supabase.co`)
- **Anon (public) key** → `NEXT_PUBLIC_SUPABASE_ANON_KEY`
- **Service role key** (server-only, for seeding) → `SUPABASE_SERVICE_ROLE_KEY`

Get them from **Dashboard → Project Settings → API** ([supabase.com/dashboard/project/_/settings/api](https://supabase.com/dashboard/project/_/settings/api)).

## One-time database setup

**Option A – SQL Editor (no token)**  
1. Open [Supabase SQL Editor](https://supabase.com/dashboard/project/_/sql/new).  
2. Run the contents of **`supabase/seed.sql`**.  
3. Run each file in **`supabase/migrations/`** in order (001 → 010) if you use migrations.

**Option B – Management API (with PAT)**  
1. Create a [Personal Access Token](https://supabase.com/dashboard/account/tokens) with **database_write**.  
2. Run: `SUPABASE_ACCESS_TOKEN=your_pat npm run db:seed`

**Option C – CLI**  
1. Run `npx supabase login`, then `npx supabase link --project-ref <your-project-ref>` (use your DB password when prompted).  
2. Run `npm run db:push`.

After any option, enable **Realtime** for the **`blocks`** table:  
**Database → Replication** → enable **blocks** for your project.

## What gets created

| Item | Purpose |
|------|---------|
| **profiles** | One row per user (created by trigger on signup). |
| **workspaces** | One per user on signup; identified by `slug` in the URL. |
| **workspace_members** | Membership + role (owner / editor / viewer). |
| **blocks** | All doc content (pages, text, lists, etc.); tree via `parent_id` and `content` (child IDs). |
| **block-assets** bucket | File uploads for blocks; path `{workspace_id}/{block_id}/{filename}`. |
| **RLS** | Access only to workspaces you’re a member of; storage scoped by workspace. |
| **Functions** | `get_block_descendants`, `get_workspace_blocks`, `is_workspace_member`, `get_workspace_role`. |

## Auth callback URL

OAuth redirect is set to `NEXT_PUBLIC_SITE_URL/auth/callback` (or the request origin if not set). Ensure your app serves that path (e.g. `http://localhost:3000/auth/callback` in dev). In **Supabase Dashboard → Authentication → URL Configuration**, add the same URL under **Redirect URLs**.
