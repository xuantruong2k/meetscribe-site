# meetscribe-site

Source for the MeetScribe landing page at <https://meetscribe.goldenpaw.org>. A single `index.html` plus a handful of static assets — no framework, no build step.

## Local changes

Open `index.html` in any browser. That's the entire development loop. No `npm install`, no dev server, no watchers.

## Deploy

Push to `main`. The `.github/workflows/deploy.yml` workflow runs on every push and uploads the repo to Cloudflare Pages via `wrangler pages deploy` (the Pages project is in Direct Upload mode — there is no Cloudflare-side Git integration). End-to-end takes ~30–60 seconds, plus the 5-minute HTML cache TTL from `_headers` before changes are fully live for all visitors.
