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

Set `SMTP_PASS` to a Gmail App Password for `bridge4er@gmail.com`. Gmail will not accept the normal mailbox password for SMTP. Keep `ADMIN_TOKEN` private; the admin panel uses it to save recipients, thresholds, and trigger manual DHM polls.

The bot polls DHM every 10 minutes and stores data in `data/state.json`.
