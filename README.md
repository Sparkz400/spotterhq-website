# SpotterHQ Website

Static marketing site for `https://spotterhq.app`, deployed via GitHub Pages.

## Deep Link Rollout Files

- `/.nojekyll` ensures GitHub Pages publishes dotfiles and `/.well-known/*`.
- `/.well-known/assetlinks.json` is the Android App Links statement list.
- `/.well-known/apple-app-site-association` is the iOS Universal Links file.
- `/404.html` doubles as the deep-link fallback page for supported entity routes.

## Required Post-Deploy Steps

1. Replace `REPLACE_WITH_PLAY_APP_SIGNING_SHA256` in
   `/.well-known/assetlinks.json` with the production Google Play App Signing
   SHA-256 fingerprint from Play Console.
2. Add a Cloudflare response-header override for
   `/.well-known/apple-app-site-association`:
   - `Content-Type: application/json`
   - no redirect on the path
   - preserve direct `200 OK` from `https://spotterhq.app`
3. Replace the placeholder iOS store URL in the website and app once the real
   numeric App Store ID is available.
4. Validate:
   - Android Digital Asset Links via Google's Statement List Generator/Tester
   - iOS Universal Links via `swcutil` or Apple's validation path
