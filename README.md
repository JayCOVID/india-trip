# India Travel PWA — Deployment Guide

## What's in this folder
- `index.html` — The entire travel app (passports, visas, flights, checklist)
- `sw.js` — Service worker (makes it work offline + auto-update)
- `manifest.json` — PWA manifest (home screen icon, app name)
- `icons/` — App icons for home screen

## Deploy to GitHub Pages (free, 5 minutes)

### Step 1: Create a GitHub account (skip if you have one)
1. Go to **github.com** → Sign up
2. Verify your email

### Step 2: Create a new repository
1. Go to **github.com/new**
2. Repository name: `india-trip` (or whatever you want)
3. **IMPORTANT:** Set it to **Private** (this has passport numbers!)
4. Click **Create repository**

### Step 3: Upload the files
1. On your new repo page, click **"uploading an existing file"** link
2. Drag and drop ALL 4 items from this folder:
   - `index.html`
   - `sw.js`
   - `manifest.json`
   - `icons/` folder (with both SVG files inside)
3. Click **Commit changes**

### Step 4: Enable GitHub Pages
1. Go to your repo → **Settings** tab (top menu)
2. In the left sidebar, click **Pages**
3. Under "Source", select **Deploy from a branch**
4. Branch: **main**, folder: **/ (root)**
5. Click **Save**
6. Wait ~60 seconds, then refresh. You'll see a URL like:
   `https://YOUR-USERNAME.github.io/india-trip/`

### Step 5: Add to your iPhone home screen
1. Open that URL in **Safari** on your iPhone
2. Tap the **Share** button (square with arrow)
3. Scroll down → tap **"Add to Home Screen"**
4. Name it "India Trip" → tap **Add**
5. Done! It now looks and works like a native app

### Step 6: Share with family
- **Swathi:** Send her the URL. She does the same Share → Add to Home Screen.
- **Anjani:** Same process — or open it once on her phone and it'll work offline after that.

## How to update the travel info later
1. Edit `index.html` on GitHub (click the file → pencil icon → edit)
2. Change the data in the `TRAVELERS`, `OUTBOUND`, `RETURN`, or `CHECKLIST` arrays
3. In `sw.js`, change `india-travel-v1` to `india-travel-v2` (this triggers the update)
4. Commit. Next time anyone opens the app with internet, they'll see "Updated travel info available — tap to refresh"

## How offline works
- First visit: downloads and caches everything
- No internet: serves from cache — everything works
- Back online: checks for updates in background, shows banner if new version found
- The checklist state is saved locally on each device

## Security note
The app is protected by a 4-digit PIN lock screen. The PIN is stored as a SHA-256 hash — the actual PIN does not appear anywhere in the code. Once a device enters the correct PIN, it's remembered permanently on that device (via localStorage).

To change the PIN later:
1. Generate a new SHA-256 hash of your new PIN at any SHA-256 tool online
2. Replace the hash value in the `PIN_HASH` variable in `index.html`
3. Bump the cache version in `sw.js`
4. Commit to GitHub

The repo can be public since no one can view the data without the PIN.
