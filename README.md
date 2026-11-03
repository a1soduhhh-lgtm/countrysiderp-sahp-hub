# CountrysideRP Nevada DPS SAHP Hub — upgraded

Node.js/Express website with a public department portal and a password-protected command dashboard.

## Features
- Navy-and-gold homepage, editable headings, banner, hero image, mission, about, footer and accent color.
- Admin uploads PNG/JPEG/WebP/GIF photos up to 3 MB. Images are stored in SQLite, not on temporary upload paths.
- Public Chain of Command shows only Commissioner, Deputy Commissioner, Assistant Commissioner, Chief, Assistant Chief, Captains and Lieutenants, with callsign and assigned name (or Vacant).
- Complete roster is accessible only to signed-in administrators. Prepopulated callsign slots match the supplied rank structure. Duplicate 5460 was included only once; 5450 and 5461 were not supplied and are not invented.
- Admin can edit roster assignments, announcements, promotions, ranks, vehicles, uniforms, training, policies, resources, and other published sections.
- Existing password/session/CSRF protections remain in place.

## Deploy on your existing Render service
1. Download this ZIP and **extract it** on your computer.
2. Open your existing GitHub repository and upload the **contents** of this folder to the repository root, replacing existing `server.js`, `package.json`, and `public/` files. Do not upload the ZIP as a single file.
3. Keep existing Render environment variables: `NODE_VERSION=22.16.0`, `ADMIN_PASSWORD`, and `SESSION_SECRET`. Do not put secrets in GitHub.
4. Render should redeploy from the main branch. Visit your existing onrender.com URL and hard-refresh.
5. Use Command Login → Administration → Website Editor, Pages & Posts, Private Roster, or Security.

## CRITICAL: permanent storage
The app defaults to SQLite at `hub.db` inside the application directory. Render's **free** filesystem is ephemeral: uploaded images, roster changes, and edits can be lost on restart or redeploy. **Do not treat the current free Render setup as permanent storage.** To make changes persistent, provision a persistent disk on a compatible paid Render service and set `DB_PATH` to a file path on that disk (for example `/var/data/hub.db`). The service must be restarted after changing `DB_PATH`. Alternatively, migrate this application to an external managed database before using it for real records. Back up the database regularly. Never commit `hub.db` or secrets to GitHub.

If the previous version already contains data in `hub.db`, migrate or back it up before changing storage; this release adds tables without intentionally deleting existing records. Existing old roster entries are excluded from the public API, and new roster slots are managed separately.

All displayed department information is for a fictional FiveM roleplay community.
