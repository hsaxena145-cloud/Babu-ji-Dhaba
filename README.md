# Babu Ji Family Dhaba — app source

## Included
- Hindi/English food menu, search and category filters
- Cart, pickup/delivery billing, WhatsApp order message
- PIN-protected admin endpoints, order status, menu availability/addition
- Order history, PWA manifest/service worker
- Capacitor Android wrapper and GitHub Actions workflow to produce a debug APK

## Run locally
1. Install Node.js 20 or newer.
2. Copy `.env.example` to `.env`.
3. Set `ADMIN_PIN` to a strong private PIN and set `WHATSAPP_NUMBER` to the restaurant's full country-code number (digits only, e.g. 91XXXXXXXXXX).
4. Run `npm install`, then `npm start`; open `http://localhost:3000`.

## APK build using GitHub (phone-friendly)
1. Upload this project's ZIP contents into the root of a GitHub repository (not inside an extra nested folder).
2. Open the repository's **Actions** tab and enable workflows if asked.
3. Run **Build Android APK** using **Run workflow**, or push to `main`.
4. Open the completed workflow run, go to **Artifacts**, download `babuji-dhaba-debug-apk`, and extract `app-debug.apk`.

## Important limitations / deployment notes
- This is a debug APK, not a Play Store signed release.
- The Android APK uses the local web app; for orders across devices, deploy `server.js` to a public HTTPS host and configure the app's API base URL before production. The current frontend calls relative `/api/...` endpoints and is therefore intended to run with the server at the same origin.
- JSON-file storage is a small starter setup, not suitable for reliable multi-instance production hosting. Use MongoDB/PostgreSQL and backups before taking real customer orders.
- Online payment endpoints verify Razorpay signatures on the server, but the online checkout UI is deliberately not enabled yet; implement and test the Razorpay checkout flow before accepting payments.
- Change admin PIN; do not commit `.env` or live keys. Never place Razorpay secret in frontend code.
