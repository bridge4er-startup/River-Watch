# River Watch

River Watch monitors three DHM hydrology stations and sends email alerts when an admin-defined warning or danger river stage is crossed.

- 265, Thulo Bheri at Rimna: https://dhm.gov.np/hydrology/hms-Single/145
- 267, Sano Bheri at Simlighat: https://dhm.gov.np/hydrology/hms-Single/162
- 268, Saru Gad at Jajarkot: https://dhm.gov.np/hydrology/hms-Single/4791

## Run

```bash
copy .env.example .env
npm start
```

Set `SMTP_PASS` to a Gmail App Password for `riverwatch2083@gmail.com`. Gmail will not accept the normal mailbox password for SMTP. Keep `ADMIN_TOKEN` private; the admin panel uses it to save recipients, thresholds, trigger manual DHM polls, and send immediate emergency emails.

The bot polls DHM every 10 minutes and stores data in `data/state.json`.

## GitHub Pages

The public site is deployed from the `public/` folder by `.github/workflows/river-watch.yml` to https://bridge4er-startup.github.io/River-Watch/. The workflow polls DHM every 10 minutes, writes the browser-ready snapshot to `public/data/snapshot.json`, commits refreshed data, and deploys GitHub Pages.

Repository: https://github.com/bridge4er-startup/River-Watch

GitHub Pages is static, so it cannot safely store email addresses, change thresholds, or send Gmail directly by itself. Deploy `server.js` as a Node service and set the repository variable `PUBLIC_API_BASE` to that service URL so the static page can call the API.

Set these backend environment variables before relying on website signup, admin actions, or email alerts:

- `SMTP_PASS`: Gmail App Password for `riverwatch2083@gmail.com`
- `ADMIN_TOKEN`: private password for admin API actions
- `PUBLIC_API_BASE`: public URL of the deployed Node API
- `CORS_ORIGIN`: `https://bridge4er-startup.github.io`

Alert emails are sent to the configured recipients plus the admin email, `riverwatch2083@gmail.com`, when a station reaches warning or danger level.

## Website Actions

- Visitors can add their email address from the website. The backend saves it in `data/config.json`.
- Admins can enter the admin password to change warning and danger levels.
- Admins can send an immediate emergency email to every saved recipient.
