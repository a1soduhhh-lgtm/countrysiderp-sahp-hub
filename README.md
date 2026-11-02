# CountrysideRP Nevada DPS SAHP Hub

A public department information website with a password-protected administration panel. Not a CAD system.

## Local start

1. Install Node.js 20+.
2. In this directory run `npm install`.
3. Set environment variables `ADMIN_PASSWORD` (12+ characters) and `SESSION_SECRET` (a long random value). Optionally set `ADMIN_USERNAME` (defaults to `admin`). Copy `.env.example` for reference; the app does **not** load `.env` automatically.
4. Run `npm start` and open `http://localhost:3000`.
5. Click **Command Login** to edit pages, promotions, uniforms, vehicles, ranks, roster entries, and more.

On Windows PowerShell:
```powershell
$env:ADMIN_PASSWORD="your-long-private-password"
$env:SESSION_SECRET="a-different-long-random-secret"
npm install
npm start
```

## Deployment

Deploy as a persistent Node.js service (Node 20+), set the environment variables above, and use HTTPS. The default SQLite file `hub.db` is stored in the app folder; for hosting platforms with ephemeral filesystems, mount persistent storage and set `DB_PATH=/path/on/persistent/disk/hub.db`. **Without persistent storage, your edits may disappear on restart or redeploy.** Do not upload `hub.db` to a public repository. Configure regular backups. `SESSION_SECRET` must stay consistent across restarts; changing it logs everyone out.

Security notes: passwords are bcrypt-hashed; admin edits require a login and a CSRF token; login attempts are rate-limited. For larger deployments, replace the default in-memory session store with a persistent session store, use a production reverse proxy with HTTPS, and consider additional account security (2FA, individual staff accounts). The app starts with one admin account; it does not yet offer multiple roles or image file uploads. Image entries accept HTTPS URLs. All roster data is public, so do not publish private member information.

All content is sample data until your command staff edits it. This is a fictional FiveM roleplay community portal, not an official Nevada DPS site.
