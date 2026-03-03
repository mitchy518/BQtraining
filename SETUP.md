# BQ Training PWA — Strava Setup Guide

## Quick Deploy to Netlify (5 minutes)

### Step 1: Create a Strava API App

1. Go to [strava.com/settings/api](https://www.strava.com/settings/api)
2. Fill in the form:
   - **Application Name:** BQ Training
   - **Category:** Training
   - **Website:** Your Netlify URL (you can update this later)
   - **Authorization Callback Domain:** Your Netlify domain (e.g., `your-site-name.netlify.app`)
3. Save — you'll get a **Client ID** and **Client Secret**

### Step 2: Deploy to Netlify

1. Go to [app.netlify.com](https://app.netlify.com) and sign up/log in
2. Drag and drop the entire `bq-pwa-strava` folder onto the Netlify dashboard
3. Your site goes live instantly at a URL like `random-name.netlify.app`

### Step 3: Add Environment Variables

1. In Netlify, go to **Site settings → Environment variables**
2. Add two variables:
   - `STRAVA_CLIENT_ID` → paste your Client ID from Step 1
   - `STRAVA_CLIENT_SECRET` → paste your Client Secret from Step 1
3. **Redeploy** the site (Deploys → Trigger deploy)

### Step 4: Update Strava Callback Domain

1. Go back to [strava.com/settings/api](https://www.strava.com/settings/api)
2. Update **Authorization Callback Domain** to your Netlify domain (e.g., `your-site-name.netlify.app`)
   - Just the domain, no `https://` or trailing slash

### Step 5: Install on iPhone

1. Open your Netlify URL in **Safari** on your iPhone
2. Tap the **Share** button (square with arrow)
3. Scroll down and tap **Add to Home Screen**
4. The app appears on your home screen with the BQ icon

### Step 6: Connect Strava

1. Open the app and tap **⬡ Strava** in the top nav
2. Tap **Connect with Strava**
3. Enter your Client ID when prompted (first time only)
4. Authorize the app on Strava's website
5. Your runs, pace, heart rate, and weekly mileage will appear!

---

## What You Get

- **Weekly Mileage** — Last 4 weeks of running totals, time, and average HR
- **Recent Runs** — Last 10 runs with distance, pace, time, and heart rate
- **Auto-refresh** — Data loads automatically when you open the Strava panel
- **Token management** — Access tokens refresh automatically, no re-login needed

## File Structure

```
bq-pwa-strava/
├── index.html          ← Main app (all 72 weeks + Strava)
├── sw.js               ← Service worker (offline support)
├── manifest.json       ← PWA manifest (home screen install)
├── icon-192.png        ← App icon (small)
├── icon-512.png        ← App icon (large)
└── netlify/
    └── functions/
        └── strava-auth.js  ← OAuth token exchange (serverless)
```

## Troubleshooting

**"Connection failed" error:**
- Make sure environment variables are set in Netlify
- Redeploy after adding variables
- Check that your callback domain matches exactly

**"Session expired" message:**
- The app will try to auto-refresh tokens
- If it persists, disconnect and reconnect Strava

**No heart rate data showing:**
- HR data requires a chest strap or watch with optical HR
- Strava must have HR permission enabled for your device

**Can't install to home screen:**
- Must use Safari on iOS (Chrome won't work for PWA install)
- The site must be served over HTTPS (Netlify does this automatically)
