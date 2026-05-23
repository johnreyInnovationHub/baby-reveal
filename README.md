# 🌸 Baby Escape Room — Gender Reveal Web App

A magical escape room-style gender reveal for **Papi Ramon & Momma Alyn's** baby! 🎉

## 🗺️ Game Flow

1. **Landing Page** — Welcome screen with parents' names & attendees
2. **Quest 1: The Lullaby** — Answer 4 lullaby trivia questions → Unlocks word: **SWEET**
3. **Quest 2: Baby Tool Kit** — Matching game with baby items → Unlocks word: **LITTLE**
4. **Quest 3: Bet on Your Baby** — Fun baby trivia quiz → Unlocks word: **MAGIC**
5. **Quest 4: Baby Riddle** — Solve 3 baby riddles → Unlocks word: **MIRACLE**
6. **Final Quest: Baby Code** — Enter all 4 words → 10-second countdown → Spin reveal → **IT'S A GIRL! 🎀**

**The Baby Code:** `SWEET LITTLE MAGIC MIRACLE`

## 👥 Attendees

| Person | Role |
|--------|------|
| Ninong Pogi | ⭐ Game Master (solo) |
| Ninang Wishelle | 💜 Team Player |
| Ninang She | 💜 Team Player |

## 🔑 Game Master Access

- Go to `/gamemaster` or click "Game Master?" on the landing page
- Password: `ninongpogi2025`
- Game Master can: view live progress, see answer key, reset game

---

## 🚀 Setup & Deployment

### Step 1: Firebase Setup

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **"Add project"** → name it (e.g., `baby-reveal`)
3. In your project, go to **Build > Realtime Database**
4. Click **"Create Database"** → choose a region → Start in **test mode**
5. Go to **Project Settings** (gear icon) → **Your apps** → click **Web icon `</>`**
6. Register app, then copy the `firebaseConfig` values

### Step 2: Local Setup

```bash
# Clone or unzip your project
cd gender-reveal

# Install dependencies
npm install

# Create environment file
cp .env.example .env.local

# Edit .env.local and paste your Firebase values
# Then run locally:
npm run dev
```

### Step 3: Deploy to Vercel

**Option A — Via GitHub (recommended):**
1. Push your project to a GitHub repository
2. Go to [vercel.com](https://vercel.com) → New Project → Import from GitHub
3. Select your repo
4. Add environment variables (copy from your `.env.local`):
   - `VITE_FIREBASE_API_KEY`
   - `VITE_FIREBASE_AUTH_DOMAIN`
   - `VITE_FIREBASE_DATABASE_URL`
   - `VITE_FIREBASE_PROJECT_ID`
   - `VITE_FIREBASE_STORAGE_BUCKET`
   - `VITE_FIREBASE_MESSAGING_SENDER_ID`
   - `VITE_FIREBASE_APP_ID`
5. Click **Deploy**!

**Option B — Via Vercel CLI:**
```bash
npm install -g vercel
vercel login
vercel --prod
# Follow prompts, add env vars when asked
```

### Step 4: Firebase Security Rules (After Testing)

In Firebase Console → Realtime Database → Rules, update to:
```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```
(For a private party, test mode rules are fine!)

---

## 🎮 How to Play

1. Share the Vercel URL with **Ninang Wishelle** and **Ninang She**
2. **Ninong Pogi** uses `/gamemaster` to monitor progress
3. The team plays together on one shared device (or separate — Firebase syncs progress!)
4. Complete quests in order (each unlocks after the previous is done)
5. After all 4 quests, go to **Final Quest** and enter: `SWEET LITTLE MAGIC MIRACLE`
6. Watch the 10-second countdown and spin reveal — **IT'S A GIRL! 🎀**

---

## 🛠️ Customization

To change game content, edit `src/lib/gameData.js`:
- Change quest questions
- Update secret words (also update `FINAL_QUEST.code`)
- Change the gender in `GENDER = 'GIRL'`
- Add more riddles or quiz questions

---

Made with 💗 for Papi Ramon & Momma Alyn's little princess!
