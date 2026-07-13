# Attendance Tracker — PWA → APK

## What's in this folder
- `index.html` — the app (rename kept as index.html since that's what PWA/APK
  build tools expect by default)
- `manifest.json` — app name, icons, colors, standalone display mode
- `sw.js` — service worker, caches the app shell so it works fully offline
- `icon-192.png`, `icon-512.png` — regular icons
- `icon-192-maskable.png`, `icon-512-maskable.png` — maskable icons (Android
  adaptive icon safe-zone)

All attendance data still lives only in the browser's localStorage on the
device — nothing changed there, the PWA layer just makes it installable.

## 1. Host it somewhere with HTTPS
Service workers only run on HTTPS (or `localhost`). Easiest free options:
- GitHub Pages
- Netlify / Vercel (drag-and-drop the folder)
- Cloudflare Pages

Upload all files in this folder together, keeping them in the same directory
(don't put the icons or manifest in a subfolder).

## 2. Turn it into an APK
Once it's hosted, use **PWABuilder** (no install required):
1. Go to https://www.pwabuilder.com
2. Paste your hosted URL and click "Start"
3. It will read `manifest.json` and `sw.js` automatically and score the PWA
4. Click "Package for stores" → choose **Android** → download the APK/AAB

This wraps your PWA in a Trusted Web Activity (TWA) — a real Android app
that renders your site full-screen with no browser UI.

### Alternative: Bubblewrap (command line)
```bash
npm i -g @bubblewrap/cli
bubblewrap init --manifest=https://yourdomain.com/manifest.json
bubblewrap build
```
This also produces a signed APK you can sideload or upload to the Play Store.

## 3. Test before building
Open the hosted site on an Android phone in Chrome — you should see an
"Install app" / "Add to Home screen" prompt. If that shows up and the app
opens full-screen with no address bar, the APK build will work the same way.

## Notes
- If you rename `index.html`, update `start_url` in `manifest.json` to match.
- Icons are simple generated placeholders — swap `icon-192.png` /
  `icon-512.png` (and the maskable pair) for your own artwork any time,
  same filenames, same sizes.
