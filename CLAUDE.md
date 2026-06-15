# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

The source for the MeetScribe landing page at <https://meetscribe.goldenpaw.org>. A single static `index.html` plus a handful of supporting files. **No framework, no build step, no `package.json`.** If you find yourself running `npm install`, adding a bundler, or introducing JS dependencies, stop — that contradicts a load-bearing project decision (see "Static-only" below).

The main MeetScribe app source lives in a separate `meet-scribe` repo. This repo is *only* the marketing page.

## Develop / deploy loop

- **Local dev:** open `index.html` in a browser. That's it. There is no dev server.
- **Deploy:** push to `main`. Cloudflare Pages auto-deploys in ~30s. The `Cache-Control` in `_headers` gives HTML a 300s TTL, so changes go fully live within ~5 minutes.
- **Preview deploys:** opening a PR against `main` produces a `<branch>.meetscribe-site.pages.dev` preview automatically.
- **Rollback:** Cloudflare dashboard → Pages → Deployments → "Rollback to this deployment". Do not revert via `git` for production hotfixes.
- **There are no tests, no linter, no typecheck.** Validation is "open the page, click every link, run Lighthouse from DevTools (target ≥95 on all four axes)."

## Static-only — the core constraint

Decisions baked into this repo (do not relitigate without explicit user direction):

- Plain HTML/CSS/SVG. No SPA framework (React/Vue/Svelte/htmx), no bundler, no TS.
- The page must remain fully usable with JavaScript disabled. The only JS in `index.html` is a tiny platform-detection sniff that adds a CSS class — purely decorative.
- Hosting is **Cloudflare Pages**. Not Vercel, not Netlify, not a VPS.
- CSS and the small JS block live **inline** in `index.html` on purpose. Adding a Content-Security-Policy header therefore requires `'unsafe-inline'`, which defeats the point — so no CSP unless the inline blocks are first extracted into `styles.css` + `app.js`.
- Production domain: `meetscribe.goldenpaw.org` (Cloudflare-managed zone). The bare `goldenpaw.org` is a separate site; do not add a redirect between them.

## Cloudflare Pages config files

These look like normal files but are Cloudflare-specific — edit with care:

- `_headers` — per-path response headers. Splits long-cache (`/assets/*`) from short-cache (`/index.html`) so updates propagate quickly while assets stay cacheable. Also sets the security headers (HSTS, X-Frame-Options, Permissions-Policy opt-out of FLoC/Topics).
- `_redirects` — redirect rules. Currently empty.
- `404.html` — served automatically by Cloudflare Pages for unknown paths.
- `robots.txt` — intentionally has no `Sitemap:` directive (one-page site).

## What lives where

- `index.html` — the entire page. Hero, product preview mockup, "why this exists", provider cards, cost table, flow diagram, fit Yes/No, footer.
- `assets/meetscribe-icon.svg` — favicon + header brand mark (26×26).
- `assets/meetscribe-mark.svg` — smaller mark used inside the in-page app screenshot (22×22).
- `PRIVACY.md` — currently a stub; linked from the footer. Full content is a known follow-up.
- `research/` — **gitignored.** Internal planning docs (notably `landing-page-deploy-site.md`, the full deploy plan with rationale). Do not commit; do not link to it from the public site.

## Editing index.html — gotchas

- **Maintainer email** in the footer is a plain `mailto:` (`xuantruong2k@gmail.com`). Cloudflare's Email Obfuscation feature will wrap it server-side when serving — do **not** paste back the rendered `/cdn-cgi/l/email-protection#...` markup or the `cloudflare-static/email-decode.min.js` script tag. That's the "rendered output put back into source" trap; it renders `[email protected]` literally when JS is off and 404s the script locally.
- **Version + commit** in the footer (currently `v0.1.3` / `710a121`, inside a commented-out `.foot-meta` block) are manual. A `<!-- BUMP ON EACH RELEASE -->` comment marks the spot.
- **Downloads** live in the hero `.downloads` block — two OS groups (`.dl-group`), each labelled (`.dl-os`) with the platform glyph, holding real `<a class="btn …">` links. Four artifacts ship per release from `github.com/xuantruong2k/meetscribe-release/releases/download/<tag>/`: `MeetScribe-<ver>-win-Setup.exe`, `-win-Portable.zip`, `-mac-arm64.dmg` (Apple Silicon), `-mac-x86_64.dmg` (Intel). **Bumping a release = edit those four `href`s** (currently `v0.1.3`). Do **not** auto-detect Mac architecture in JS — `navigator.userAgentData` reports Apple Silicon as Intel, so both `.dmg` buttons stay visible and the `.dl-hint` line helps users pick. The `.is-mac` class only *shifts* the accent (Windows installer `.primary` → macOS `.btn-mac-primary`); it never hides a button (JS-disabled must still show all four).
- **macOS ships unsigned** (ad-hoc, not notarized), so first launch trips Gatekeeper's "MeetScribe is damaged". The hero `.gatekeeper` `<details>` carries the interim bypass (`xattr -cr …` + System Settings steps). Drop that whole block once Developer ID signing + notarization land. The unused `.btn.is-soon` CSS utility is left in place for any future not-yet-shipped button.
- **App-preview screenshot** uses macOS traffic-light chrome with a `<figcaption>` reading "macOS build pictured." (Both platforms now ship.) If/when a Windows-chrome variant lands, drop or adjust the caption.
- **OG image** (`og:image`) is not yet wired. Adding `assets/og.png` (1200×630) + the four `og:image` / `twitter:image` meta tags is a tracked follow-up, not a blocker.

## Explicitly out of scope

Do not add any of the following without re-opening the discussion:

- A blog, changelog, `/news`, `/docs`, or pricing page.
- Email signup forms beyond a `mailto:` link.
- A "Compare to Granola / Otter" page (the Yes/No fit block handles this).
- Google Analytics, Mixpanel, Segment, Amplitude, or any third-party tag manager. Cloudflare Pages' built-in server-side analytics is sufficient. Anything client-side contradicts the page's pitch.
- Any JS framework or build tooling.

<!-- SPECKIT START -->
For additional context about technologies to be used, project structure,
shell commands, and other important information, read the current plan
<!-- SPECKIT END -->
