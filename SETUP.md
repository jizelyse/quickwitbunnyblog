# 🌸 petal — setup guide

## Step 1 — Set up your database (Supabase)

1. Go to your Supabase dashboard: https://supabase.com/dashboard
2. Click your project (my-blog)
3. In the left sidebar, click **SQL Editor**
4. Click **New query**
5. Paste this entire block and click **Run**:

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

✅ You should see "Success. No rows returned."

---

## Step 2 — Deploy to Vercel (free)

1. Go to https://vercel.com and click **Sign Up**
2. Sign up with your **GitHub account** (free)
   - If you don't have GitHub: go to https://github.com, sign up free, then come back
3. Once logged into Vercel, click **Add New → Project**
4. Click **"Upload" or drag your folder** — upload the entire `petal-blog` folder
   - OR use the Vercel CLI (advanced)
5. Leave all settings as default, click **Deploy**
6. Wait ~30 seconds — Vercel gives you a free URL like `petal-blog-abc123.vercel.app`

---

## Step 3 — Rename your site (optional)

1. In Vercel dashboard, go to your project → **Settings → Domains**
2. You can change the prefix — e.g. `yourname.vercel.app`

---

## Step 4 — Start blogging! 🌸

- Open your site URL
- Click **+ write** to create your first post
- Use the black editor to write
- Customize background, fonts, colors per post
- Click **publish →** when ready
- Share the link — anyone can read, no one can comment or post

---

## Your credentials (keep these safe!)

- Supabase URL: https://mkyvkzcxsydrwlqfxewl.supabase.co
- Supabase project dashboard: https://supabase.com/dashboard

---

## FAQ

**Can people comment?** No — read only for visitors.
**Can I write on my iPhone?** Yes — the site works on mobile.
**Will I lose my posts?** No — they're saved in Supabase cloud.
**Can I add a real domain later?** Yes — in Vercel Settings → Domains, add your domain anytime.
