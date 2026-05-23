# 🌸 Baby Escape Room — Gender Reveal Web App

A magical escape room-style gender reveal for **Papi Ramon & Momma Alyn's** baby!  
Built with **React + Supabase + Vercel**.

## 🗺️ Game Flow

1. **Landing Page** — Welcome screen with parents' & attendees' names
2. **Quest 1: The Lullaby** → Secret word: **SWEET**
3. **Quest 2: Baby Tool Kit** → Secret word: **LITTLE**
4. **Quest 3: Bet on Your Baby** → Secret word: **MAGIC**
5. **Quest 4: Baby Riddle** → Secret word: **MIRACLE**
6. **Final Quest: Baby Code** — Enter `SWEET LITTLE MAGIC MIRACLE` → 10s countdown → spin reveal → **IT'S A GIRL! 🎀**

**Game Master password:** `ninongpogi2025` (go to `/gamemaster`)

---

## 🚀 Setup Guide

### Step 1 — Supabase (database)

1. Go to [supabase.com](https://supabase.com) and create a free account
2. Click **"New project"**, give it a name like `baby-reveal`, set a password, choose a region
3. Wait ~1 minute for it to spin up
4. In the left sidebar, click **"SQL Editor"**
5. Paste and run this SQL to create the game table:

```sql
-- Create the game state table
create table game_state (
  id integer primary key default 1,
  quests jsonb default '{}'::jsonb,
  revealed boolean default false
);

-- Insert the initial row
insert into game_state (id, quests, revealed) values (1, '{}', false);

-- Allow public read/write (this is a private party app, so that's fine)
alter table game_state enable row level security;
create policy "Public access" on game_state for all using (true) with check (true);

-- Enable real-time updates
alter publication supabase_realtime add table game_state;
```

6. Go to **Settings → API** and copy:
   - **Project URL** (looks like `https://abcdef.supabase.co`)
   - **anon public** key (the long string under "Project API keys")

### Step 2 — Local setup

```bash
cd gender-reveal
npm install

# Create your env file
cp .env.example .env.local
```

Open `.env.local` and paste your values:
```
VITE_SUPABASE_URL=https://your-project-id.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key-here
```

Then run locally:
```bash
npm run dev
```

Open `http://localhost:5173` — you should see the landing page! ✅

### Step 3 — Deploy to Vercel

**Push to GitHub first:**
```bash
git init
git add .
git commit -m "Baby reveal app"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/baby-reveal.git
git push -u origin main
```

**Then deploy on Vercel:**
1. Go to [vercel.com](https://vercel.com) → sign in with GitHub → **"Add New Project"**
2. Import your `baby-reveal` repo
3. Click **"Environment Variables"** and add:
   - `VITE_SUPABASE_URL` → your Supabase project URL
   - `VITE_SUPABASE_ANON_KEY` → your Supabase anon key
4. Click **"Deploy"** 🎉

Your app will be live at `https://baby-reveal.vercel.app` — share with the guests!

---

## 👥 Attendees

| Person | Role |
|--------|------|
| Ninong Pogi | ⭐ Game Master — go to `/gamemaster`, password: `ninongpogi2025` |
| Ninang Wishelle | 💜 Team Player |
| Ninang She | 💜 Team Player |

## 🛠️ Customization

Edit `src/lib/gameData.js` to change:
- Quest questions and riddles
- Secret words (also update `FINAL_QUEST.code`)
- The gender: `export const GENDER = 'GIRL'`
