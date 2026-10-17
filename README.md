# RimRunnerOhio

Unofficial Ohio HS boys basketball ratings. Not affiliated with OHSAA or MaxPreps.
Live site: https://rimrunnerohio.pages.dev/ (backup copy: GitHub Pages).

## Nightly scores

`.github/workflows/nightly-scores.yml` runs `scripts/update_scores.py` at 04:30 and 12:00 UTC
(11:30 pm / 7:00 am Eastern standard time) and on manual dispatch. Before the Ohio boys season starts
(2026-11-30, `SEASON_START` in index.html) the script makes no requests. From then on it reads boys
basketball finals for the last 3 days from the MaxPreps Ohio scores-by-date page, matches them to the
schedule by MaxPreps team id + date, records them in `data/results.json` and bakes scores and W-L records
into `index.html`. The page recomputes Elo from those finals. It commits only when data changed, then
deploys to Cloudflare Pages if the `CLOUDFLARE_API_TOKEN` repository secret is set.

`firebase/` holds the Firestore rules for when the site's own Firebase project is created (not yet).
