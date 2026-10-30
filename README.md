# The Pack

A small private web app for the officers of The Pack (Questland guild): BE log, "Last BE stats" post builder, Monster Slayer posts, weekly checklist and ready-to-copy messages.

Static files only: `index.html` + `config.js`. Data, login and live updates come from Supabase.

## Deploy to GitHub Pages
1. Push this folder to the `main` branch of the repo.
2. On GitHub, open the repo and go to **Settings > Pages**.
3. Under **Build and deployment**, set **Source: Deploy from a branch**, then **Branch: `main`**, folder **`/ (root)`**, and click **Save**.
4. After 1-2 minutes the site is live at `https://<username>.github.io/the-pack/`.

## Configuration
`config.js` holds the Supabase project URL and the **publishable (anon) key**. That key is meant to be public: Row Level Security (see `schema.sql`) lets only signed-in users read or write. Never put the `service_role` / secret key in this repo.

## Data
Everything shared lives in two tables (see `schema.sql`):
- `entries`: one row per Battle Event. `data` = `{ date, color, played: [], missed: [], away: [], stats: { place, league, score, h30, h11, h6, h1 } }`. Marking who played edits the entry of the Battle Event that ended last.
- `kv`: one row per setting, so two people saving at once never overwrite each other: `member:<name>`, `left:<name>`, `prospect:<id>`, `gear:<week>:<group>`, `picks:<week>:<group>`, `be:week`, `runorder`, `done:<ISO week>:<task>`, `daily:<YYYY-MM-DD>:<task>`, `msgs:<hash>` (edited message text). A missing row means the default from the code.

The open tab, the Kaya/Ewa toggle and the undo history stay in the browser.

## Accounts
Sign-ups are disabled in Supabase. Users are created in Supabase > Authentication > Users as `<name>@thepack.app`; in the app you log in with just `<name>`.

## Run locally
```
python3 -m http.server 8080
```
Then open http://localhost:8080.
