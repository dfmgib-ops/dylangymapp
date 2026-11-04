# Gym Log — project rules

Personal gym-logging PWA used on an iPhone at the gym. No build step.

## Layout
- App files live in `gym-log-app/`: `index.html` (all HTML/CSS/JS), `sw.js`, `manifest.webmanifest`, icons.
- Hosted on Netlify, auto-deploys from `main`. Publish directory must be `gym-log-app`.

## Data — never break existing data
- All data is in localStorage under the key `"gymlog-v1"` (`KEY` in `index.html`). **Never change this key.**
- Users rely on JSON export/import. Old exports must still import.
- If the data shape needs to change, add a migration where the data is loaded (the `load` code that reads `KEY`) so older data and imported files are upgraded in place. Don't drop or rename fields without migrating.
- The program is embedded as `DEFAULT_PROGRAM` in `index.html` (Mon/Wed/Fri). It has a `version` field that can be used to detect old data.

## Service worker
- Whenever any app file changes, bump `CACHE` in `gym-log-app/sw.js` (e.g. `gymlog-v1` → `gymlog-v2`) so the phone picks up the update.
- `CACHE` is unrelated to the localStorage key, even though both started as `gymlog-v1`. Bump only `CACHE`.

## Design — keep it
- Plate colours per day: red = Monday, blue = Wednesday, yellow = Friday.
- Barlow fonts.
- Large tap targets for use mid-workout on a phone.
