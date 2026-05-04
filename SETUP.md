# In Wonderland — setup guide

## Step 1 — Supabase database (one time only)

1. Go to https://supabase.com/dashboard → open your project
2. Click SQL Editor → New query
3. Paste and Run:

```sql
create table posts (
  id uuid default gen_random_uuid() primary key,
  title text,
  slug text unique,
  body text,
  tag text,
  bg text default '#ffffff',
  status text default 'draft',
  created_at timestamptz default now()
);
alter table posts enable row level security;
create policy "public read" on posts for select using (true);
create policy "public write" on posts for all using (true);
```

✅ "Success. No rows returned."

---

## Step 2 — Enable Google Login in Supabase

1. In Supabase dashboard → Authentication → Providers
2. Click Google → Enable it
3. You need a Google OAuth Client ID and Secret:
   - Go to https://console.cloud.google.com
   - Create a project → APIs & Services → Credentials → Create OAuth Client ID
   - Application type: Web application
   - Authorized redirect URI: https://mkyvkzcxsydrwlqfxewl.supabase.co/auth/v1/callback
   - Copy the Client ID and Client Secret back into Supabase
4. Save

---

## Step 3 — Deploy to Vercel

1. Push this folder to a GitHub repo (see previous instructions)
2. Go to vercel.com → Import that repo → Deploy
3. Your site is live at yourname.vercel.app

---

## Step 4 — Add your Vercel URL to Supabase

1. Supabase → Authentication → URL Configuration
2. Set Site URL to: https://yoursite.vercel.app
3. Add to Redirect URLs: https://yoursite.vercel.app

---

## How it works

- Visitors see: blog posts, read them, nothing else
- You go to: yoursite.vercel.app → click "owner login" (tiny, bottom of nav)
- Sign in with jiz.elyse@gmail.com → edit/write/delete buttons appear
- Anyone else who tries to log in sees nothing extra
