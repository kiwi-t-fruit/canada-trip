# 🍁 Canada Trip

A Progressive Web App for tracking wildlife sightings and discovering restaurants & amenities during the Canada road trip.

**Live app:** https://kiwi-t-fruit.github.io/canada-trip/

---

## Setup

### 1. Clone the repo

```bash
git clone https://github.com/kiwi-t-fruit/canada-trip.git
cd canada-trip
```

### 2. Create your config file

```bash
cp config.example.js config.js
```

Then open `config.js` and fill in each user's 4-digit PIN:

```js
const USERS = [
  { name: "Kiren",        pin: "1234" },
  { name: "Sean",         pin: "5678" },
  { name: "Sasha & Matt", pin: "9012" },
];
```

> ⚠️ `config.js` is gitignored and must **never** be committed. The PINs live only on your local machine and in the GitHub secret (see below).

### 3. Open locally

Just open `index.html` in a browser. No build step required.

---

## Deploying to GitHub Pages

### First-time setup

1. Go to **Settings → Pages** in your GitHub repo and set the source to **GitHub Actions**.

2. Go to **Settings → Secrets and variables → Actions** and create a secret named `CONFIG_JS` with the full contents of your `config.js` file, e.g.:

   ```
   const USERS = [
     { name: "Kiren",        pin: "1234" },
     { name: "Sean",         pin: "5678" },
     { name: "Sasha & Matt", pin: "9012" },
   ];
   ```

3. Push to `main`. The GitHub Action will inject `config.js` from the secret and deploy automatically.

### Subsequent deploys

Just push to `main` — the action runs automatically.

---

## Firebase / Firestore

The app uses Firebase Firestore for real-time sync and offline support (via built-in persistence).

- **Project:** `canada-trip-d8749`
- **Rules:** See `firestore.rules` — currently open read/write. Tighten before sharing publicly.

To deploy updated Firestore rules:

```bash
npm install -g firebase-tools
firebase login
firebase deploy --only firestore:rules
```

---

## Features

| Feature | Description |
|---|---|
| 🐻 Wildlife Counter | Log animal sightings with GPS, timestamp, and notes |
| 📍 Directory | Restaurant & amenities finder across 6 cities |
| 🔒 PIN Auth | Three user profiles with 4-digit PINs |
| 📡 Offline sync | Writes queued in IndexedDB, synced on reconnect |
| 📱 PWA | Installable on iOS and Android home screens |

---

## Project structure

```
canada-trip/
├── index.html          # Full single-page app
├── sw.js               # Service worker (caching + offline)
├── manifest.json       # PWA manifest
├── config.js           # ← YOU create this (gitignored)
├── config.example.js   # Template for config.js
├── firestore.rules     # Firestore security rules
├── icons/
│   ├── icon-192.png
│   └── icon-512.png
└── .github/
    └── workflows/
        └── deploy.yml  # GitHub Pages deployment
```
