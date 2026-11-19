# Gilla Ore Duel Arena — Meta Quest 3S PWA

This package contains the uploaded `Gilla_Ore_Duel_Arena.html` game, wrapped as a PWA for Meta Quest.

## What's included
- `index.html` — the game HTML, retained with PWA metadata and Quest PWA auto-start logic.
- `manifest.webmanifest` — install/package metadata and launcher icons.
- `sw.js` — a small service worker shell. The game still needs an internet connection for its CDN/Firebase features.
- `icons/` — PWA launcher icons.

## Important compatibility notes
- This is a PWA source package, **not an APK**.
- Host the contents of this folder at a public HTTPS origin before using Bubblewrap.
- Test the hosted game in the Meta Quest Browser first. The game should enter immersive VR from the installed immersive PWA launch; regular browser visits retain the normal game menu.
- The HTML uses Three.js 0.147.0 and external CDN/Firebase scripts, so an internet connection is required.
- In Bubblewrap choose **immersive** app mode. Meta's current packaging flow stores this as `horizonOSAppMode` in `twa-manifest.json`.
- For Quest immersive PWAs, Meta requires valid Digital Asset Links at `https://YOUR-DOMAIN/.well-known/assetlinks.json`.

## Next packaging steps (after HTTPS hosting)
From your Chromebook Terminal:
```bash
mkdir -p ~/gilla-ore-duel
cd ~/gilla-ore-duel
# Put the hosted manifest URL into Bubblewrap init:
bubblewrap init --manifest=https://YOUR-DOMAIN/manifest.webmanifest --metaquest
```
When prompted:
1. Set app mode to `immersive`.
2. Use a unique Android package ID, for example `com.yourname.gillaoreduel` (replace `yourname` with a unique identifier).
3. Keep the generated signing keystore safe; future updates need the same key.

Then follow Meta's current Bubblewrap build and Digital Asset Links steps:
https://developers.meta.com/vr/documentation/web/pwa-packaging/

Do not run `bubblewrap init` until the HTTPS site and manifest URL are live.
