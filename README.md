# meetscribe-site

Source for the MeetScribe landing page at <https://meetscribe.goldenpaw.org>. A single `index.html` plus a handful of static assets — no framework, no build step.

## Local changes

Open `index.html` in any browser. That's the entire development loop. No `npm install`, no dev server, no watchers.

## Deploy

Push to `main`. Cloudflare Pages picks up the change automatically and publishes within ~30 seconds. The HTML cache TTL is 5 minutes (see `_headers`), so updates go fully live within ~5 minutes of a push. PRs against `main` get an auto-generated preview deploy at `<branch>.meetscribe-site.pages.dev`.
