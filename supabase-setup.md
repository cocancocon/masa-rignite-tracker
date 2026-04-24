# Supabase setup for shared team sync

## 1. Create table
Open Supabase → SQL Editor → New query, then run:

```sql
create table if not exists public.team_trackers (
  id text primary key,
  data jsonb not null,
  updated_at timestamptz default now(),
  updated_by text
);

alter table public.team_trackers enable row level security;

create policy "Allow public read for hackathon tracker"
on public.team_trackers
for select
using (true);

create policy "Allow public insert for hackathon tracker"
on public.team_trackers
for insert
with check (true);

create policy "Allow public update for hackathon tracker"
on public.team_trackers
for update
using (true)
with check (true);
```

## 2. Get keys
Go to **Project Settings → API** and copy:
- Project URL
- anon public key

## 3. Connect the tracker
Open the hosted GitHub Pages tracker → **Sync** tab.
Paste:
- your name
- Supabase Project URL
- anon public key
- one shared room ID, e.g. `masa-rignite-team-a`

The first person clicks **Push now**. Everyone else uses the same settings and clicks **Pull latest**.

## Important
This setup is intentionally simple for a short hackathon. Anyone with the website, anon key, and room ID can edit the tracker. Do not store private data here.
