# MeetScribe — Landing Page Design Notes

> **Scope:** plan for a single-page public site that introduces MeetScribe, makes the BYOK trade-off honest up front, and routes visitors to the right download. Companion to `distribution-strategy.md` — that doc explains *why* we ship BYOK; this doc explains *how to present it* to a first-time visitor.
>
> **Date:** 2026-05-08
> **Status:** design notes. Not a copy deck — but the sample copy in §4 is close enough to ship if you want.

---

## 1. What this page must do

The landing page is doing four jobs at once. Holding all four in mind is what keeps it from drifting into either generic SaaS marketing or engineer-only README dryness.

### 1.1 Set expectations honestly before the user clicks Download

The single biggest cause of bad reviews / churn for a BYOK app is the user discovering "wait, I need *two* API keys?" *after* installing. The landing page must make the two-key requirement visible **above the fold**, not buried in a setup guide. Engineers are fine with this; non-engineers self-select out — that's the goal.

> Phrased as a rule: **the friction is the feature.** Show it on the landing page.

### 1.2 Make the privacy / no-middleman story concrete

Saying "your data stays local" is what every meeting app says. The landing page wins by being **specific and verifiable**:

- Audio goes from your machine → STT provider you chose, with your key.
- Transcript text goes from your machine → LLM provider you chose, with your key.
- Nothing else leaves your machine. Ever.
- We don't run a backend. We can't see your data because there's nothing to look at.

Engineers verify these claims by watching network traffic for 30 seconds. The page should *invite* that verification, not avoid it. Link to `PRIVACY.md`. Mention Little Snitch / Wireshark by name.

### 1.3 Communicate the real cost without scaring people off

From `estimate-cost.md`:
- ≤ 10 hrs/mo of meetings → free (Gladia free tier + Gemini free tier or DeepSeek signup credit)
- 40 hrs/mo → ~$18–20/mo total, of which ~$1.69 is LLM (Gemini default) and ~$18 is STT
- Light occasional use → typically $0–$5/mo

Phrase as **"often free, usually under $20/mo, you pay providers directly."** Don't oversell free; engineers pattern-match "free" to "freemium with a catch."

### 1.4 Drive the right download

Two buttons, OS-detected default, no email gate, no signup, no newsletter capture. The download IS the conversion. Don't break that flow.

---

## 2. Page content (top to bottom)

Order matters. This is the order a privacy-conscious engineer reads in.

### 2.1 Hero

- **Headline (one sentence, ~10 words):** *"Meeting transcripts and summaries — your keys, your data, no middleman."*
- **Sub-headline (one line):** *"Local-first desktop app for Windows (macOS coming soon). Bring your own API keys."*
- **One primary download button:** `Download for Windows`. Below it, a smaller disabled-looking pill: `macOS — coming soon`. If the visitor is on macOS, surface a "Notify me when macOS ships" mailto link or GitHub-watch hint instead of a download.
- **One-line honesty hook directly below the buttons:** *"Requires two API keys (STT + LLM). Setup takes ~5 minutes. Often free for light use."*

### 2.2 What it does (the short version)

Three short bullets, no marketing voice:

- **Captures both sides of your meeting.** System audio (Zoom / Meet / Teams output) and your microphone, mixed locally. No bot joins the call. Ambient silence is filtered out on-device before anything streams, so the transcription provider never hears — or hallucinates over — dead air.
- **Streams to a transcription provider you choose.** Gladia or AssemblyAI — your key, your bill, your data.
- **Summarizes with the LLM you choose.** Gemini (default, best cost/performance), DeepSeek (cheapest), or OpenAI — your key, your bill.

Optional small screenshot or 30-second GIF: click record → live transcript → click stop → summary appears.

### 2.3 Why this app exists (the differentiator section)

This is the heart of the page. Three short blocks, each with a one-line claim and a one-line proof.

| Claim | Proof |
|---|---|
| **Your audio never touches our servers** | We don't have servers. Audio goes from your Mac/PC straight to the STT provider you picked. |
| **Your keys live in your OS keychain** | macOS Keychain on Mac. Windows Credential Manager on Windows. We never see them — there's nothing to send them to. |
| **All your meetings stay on your machine** | Transcripts and summaries are saved as plain files in your home folder. Delete the folder, the data is gone. No "cloud sync" toggle hiding somewhere. |
| **You can audit every network call** | The app makes calls to exactly three places: your STT provider, your LLM provider, the update server (only if you opt in to update checks). Watch with Little Snitch / Wireshark — that's all there is. |

### 2.4 The honest two-key explanation

A short section titled something like **"Why two API keys?"** — written in the voice of someone explaining a trade-off to a friend, not selling them on it.

Sample copy (close to ship-ready):

> *MeetScribe is a desktop app, not a hosted service. To transcribe audio it needs a transcription provider. To summarize text it needs an LLM. We don't run our own — we'd need a backend, your data would pass through our infrastructure, and we'd be on the hook for someone else's bill. Instead, you sign up for the providers you trust (or already use), paste two keys, and the app talks directly to them.*
>
> *Trade-off: ~5 minutes of setup vs. one-click. Upside: no middleman, no markup, no "we promise not to look," and you can switch providers any time without asking us.*

Below this, two side-by-side cards previewing the providers:

**STT (transcription)**
- **Gladia** — free 10 hrs/month, then ~$0.61/hr. Best for occasional use.
- **AssemblyAI** — $50 signup credit (~138 hrs free). Best if you have heavy months.

**LLM (summary)**
- **Google Gemini** — default. Best cost/performance balance. Free tier covers typical use; ~$1.69/mo after.
- **DeepSeek** — cheapest. $5 signup credit ≈ 3 months free, ~$0.31/mo after.
- **OpenAI** — pay-as-you-go, ~$1.39/mo at typical use. Strongest English / European-language quality.

Each provider name should link to the signup page (deep link if possible). Be specific about cost — engineers respect numbers, distrust adjectives.

### 2.5 Cost (one short, scannable block)

A small table, no asterisks, no fine print:

| Usage | What you'll typically pay |
|---|---|
| A few meetings a week | $0/mo (free tiers cover it) |
| ~10 hrs/mo | $0–$1/mo |
| ~40 hrs/mo | ~$15–20/mo |

Followed by one line: *"You pay providers directly. We never bill you. There is no MeetScribe subscription."*

### 2.6 How it works (3-step visual)

A simple horizontal diagram or 1-2-3 numbered list:

1. **You record** → audio captured locally (system + mic, mixed).
2. **Audio streams to your STT provider** → live transcript appears in the app.
3. **Transcript is summarized by your LLM** → summary, action items, decisions, saved as a plain file on your disk.

No backend in the diagram. The absence is the point — visualize that.

### 2.7 Quick setup (set the right expectation)

A 4-step list, terse:

1. Download for Windows (macOS coming soon).
2. Get a free STT key (Gladia or AssemblyAI).
3. Get a free LLM key (Gemini recommended for balance; DeepSeek if you want the cheapest option).
4. Paste both keys. Start recording.

End with: *"~5 minutes total. No account, no login, no email."*

### 2.8 The "is this for me?" section

A two-column "yes / no" block — fast self-selection.

**You'll like MeetScribe if:**
- You want your meeting data on your machine, not in a SaaS.
- You're comfortable signing up for two API providers.
- You want to pay only for what you use.
- You like desktop apps you can audit at the network level.

**You'll be happier with Granola / Otter / Fireflies if:**
- You want one-click setup with no API keys.
- You want shared team workspaces and integrations (Notion, Slack, calendars).
- You'd rather pay a flat $19/mo and not think about it.

This is the **most engineer-respectful** thing you can put on a landing page — telling people who aren't your audience to use a different product. It builds trust with the people who *are* your audience.

### 2.9 Honest maintenance disclosure

A short block, one paragraph, near the bottom but above the footer. Lifted from `distribution-strategy.md` §7:

> *"MeetScribe is a side project. The author uses it daily for real meetings and fixes what breaks. Issues are read but not always answered. PRs are reviewed slowly. No SLA, no roadmap, no support contract. If you need a supported product, use Granola or Otter."*

This sentence is unusual on a landing page. That's why it works — it signals the page is honest about the rest too.

### 2.10 Footer

- `PRIVACY.md` link
- **Ideas / wishlist link** — points at a public issue tracker filtered by `label:idea` (see §6 below)
- Author's name and contact (real name, real email — see §6.10 of distribution-strategy.md)

No newsletter signup. No "© 2026 MeetScribe Inc." (there is no Inc.). No analytics other than maybe Plausible/GoatCounter if you want raw download counts; if you do add analytics, mention it in the privacy section.

Note: there is **no "Roadmap" section** on the landing page — see §6 for the reasoning.

---

## 3. Visual / structural design

### 3.1 Guiding principle

> **The page itself should feel like the app: clean, fast, no dark patterns, no surprises.**

If the landing page has a chatbot widget, an exit-intent popup, or a "wait! before you go!" modal, you've broken the trust the rest of the page is trying to build. Engineers notice, and the people who don't notice aren't your audience.

### 3.2 Layout

- **Single column, centered, ~720px max content width.** Two columns only inside the "STT / LLM" cards and the "yes / no" block.
- **System fonts.** Inter / SF Pro / Segoe UI fallback stack — no Google Fonts (privacy + speed).
- **Light mode default, respect `prefers-color-scheme: dark`.** No theme switcher needed.
- **No hero image of a smiling person at a laptop.** Use a minimal product screenshot or, better, an animated SVG of the data flow (mic → app → provider).
- **Plenty of whitespace.** A landing page that looks information-dense is a landing page that looks like work.
- **All text left-aligned.** Centered paragraph text reads slower; ragged-left aligns with how docs and READMEs feel.

### 3.3 What to skip

- Customer logos ("Trusted by Acme, Globex…") — you don't have any. Don't fake it.
- Testimonials, unless you have real quotes from named users with permission.
- Animated gradients, parallax scroll, fancy hero video. They suggest "we have a marketing budget"; you don't and shouldn't.
- "Get started for free" CTAs that imply there's a paid tier. There isn't.
- Cookie banner — only needed if you set tracking cookies. Don't set tracking cookies.

### 3.4 Performance budget

- Fully usable with JS disabled. No SPA framework — plain HTML + a tiny CSS file.
- Page weight under 100KB on first load (excluding any GIF demo).
- Lighthouse 100 / 100 / 100 / 100.
- First contentful paint under 500ms on a 3G connection.

This is achievable on plain static hosting (GitHub Pages, Cloudflare Pages, Vercel). It also signals to engineers in 1 second that the team behind the page knows what they're doing — the same kind of signal as a tidy `git log`.

### 3.5 Stack recommendation (in order of "less work")

1. **Cloudflare Pages or GitHub Pages** with a single `index.html` + `style.css`. Add `og:` and `twitter:` meta tags. Ship in an hour.
2. **Astro** with one page if you want components and Markdown-driven content blocks. Slightly more setup, easier to extend with a `/changelog` or `/privacy` later.
3. **Don't:** Next.js, Gatsby, anything with hydration. It's overkill for a one-pager and will violate the perf budget.

---

## 4. Sample headline / above-the-fold copy

A drop-in starting point. Tune the verbs to your voice.

```
MeetScribe
Meeting transcripts and summaries — your keys, your data, no middleman.

Local-first desktop app for Windows (macOS coming soon).
Bring your own API keys. No subscription.

[ Download for Windows ]   macOS — coming soon

Requires two API keys (STT + LLM). Setup takes ~5 minutes.
Often free for light use, ~$15–20/month if you record 40 hrs/month.
```

---

## 5. Where to host the Windows `.exe` (macOS `.dmg` follows once the macOS build ships)

### 5.1 Recommended: GitHub Releases

**This is the right answer for a side project and matches the existing build setup.** The Windows binary ships at launch; the macOS `.dmg` slots into the same release page once the macOS build is signed and notarized.

Why:
- **Free.** No bandwidth bill, no CDN setup.
- **Already in the toolchain.** Velopack (Windows) supports GitHub Releases as a feed source out of the box (`vpk pack` produces artifacts that drop straight into a release). The eventual macOS build can attach a notarized `.dmg` to the same release.
- **Predictable URL surface.** One canonical `/releases/latest/download/...` URL per platform; never changes, never breaks.
- **Versioning is free.** Tag → Release → artifacts. Auditable changelog per release.
- **Velopack update flow** can pull from `https://github.com/<user>/meet-scribe-releases/releases/latest/download/...` — no separate update server needed. The releases repo can be public-binaries-only; the source repo can stay private.

The download links on the landing page should point to **stable URLs that always serve the latest release**, not version-specific tags. GitHub provides:

```
https://github.com/<user>/meet-scribe-releases/releases/latest/download/MeetScribe-Setup.exe
https://github.com/<user>/meet-scribe-releases/releases/latest/download/MeetScribe.dmg   # once macOS ships
```

These resolve server-side to whatever the most recent release tag has attached. Users always get current; the URL never breaks; you never have to update the landing page after a release. Until the macOS build is ready, the `.dmg` URL simply 404s — the landing page button for macOS stays disabled / "coming soon" rather than linking to it.

### 5.2 What needs to be true for the binaries

Both files must be **code-signed**, or engineers will see scary OS warnings on first launch and bounce. This is non-negotiable for a "trust me, I'm safe" pitch.

> **Interim reality (2026-05):** the macOS `.dmg` currently ships *unsigned* (ad-hoc only — no Developer ID, no notarization) while Apple Developer Program enrollment is pending, so the first launch trips Gatekeeper's "damaged" warning. §5.6 has the one-time bypass the download page must surface until then. Retire it the moment Developer ID signing + notarization land.

| Platform | Requirement | Cost / effort |
|---|---|---|
| **macOS** | Apple Developer ID signing + notarization | $99/yr Apple Developer Program. Notarization is automated via `notarytool`. Without this, Gatekeeper blocks the app. |
| **Windows** | Authenticode code signing | Either: (a) ~$200–400/yr cert from Sectigo / DigiCert / SSL.com, or (b) Azure Trusted Signing ($10/mo, no HSM hassle). Without this, SmartScreen warns users. |

Publish the **SHA256 of each artifact** in the release notes so engineers can verify. GitHub Actions artifact attestation is even better — proves the binary came from a specific commit + workflow.

### 5.3 Alternatives considered (and why not)

- **Self-host on a VPS / Cloudflare R2.** Works, but adds ops surface. No win over GitHub Releases unless you're hitting GitHub's bandwidth limits — which for a side project at side-project scale, you won't.
- **Mac App Store / Microsoft Store.** Heavy review process, sandboxing constraints (ScreenCaptureKit + audio loopback may not pass), 15–30% revenue cut on any future paid features. Not worth it for a side project.
- **Homebrew cask + winget.** Worth adding *in addition to* GitHub Releases, once releases are stable. Engineer-friendly, increases trust ("I can install with my normal tooling"). Both ultimately point at the GitHub release URL anyway.

### 5.4 Recommended release flow

1. Tag a release: `git tag v0.0.3 && git push --tags`.
2. GitHub Actions runs on tag push: builds Rust core, builds Windows app (signed + Velopack-packed). The macOS app (signed + notarized) is added to the workflow once that build path is wired up.
3. Workflow publishes artifacts to a GitHub Release with auto-generated changelog and SHA256 sums.
4. Landing page download button keeps pointing at `/releases/latest/download/MeetScribe-Setup.exe` — no edits needed.
5. Velopack picks up the new release on next opt-in update check from already-installed clients.

### 5.5 What to put in release notes

Every release. Short, predictable format. Engineers learn to skim it quickly.

- One-paragraph "what changed" summary.
- Full commit list (auto-generated).
- SHA256 hashes for `MeetScribe-Setup.exe` (and `MeetScribe.dmg` once macOS ships).
- GitHub Actions run URL + attestation (so engineers can verify the binary came from a known workflow run).
- Known issues, if any.

### 5.6 macOS first launch: Gatekeeper bypass (interim — unsigned builds)

Until Apple Developer Program enrollment completes (§5.2), the macOS `.dmg` ships **unsigned** — ad-hoc signed only, no Developer ID, no notarization. macOS Gatekeeper greets the first launch with **"MeetScribe is damaged and can't be opened."** The app is fine — that message is just Gatekeeper refusing an app without a Developer ID cert — but it reads exactly like "this is malware," which is the §5.2 bounce risk made real. So the download page must **pre-empt it inline next to the macOS button**, not bury it in a separate setup doc. Use either method once; macOS remembers the choice afterwards.

The same copy ships verbatim in every GitHub Release body (generated by `.github/workflows/macos-release.yml`) — keep the two in sync so the website and the release notes never disagree.

**Method 1 — System Settings (no Terminal):**

1. Mount the `.dmg` and drag **MeetScribe.app** to `/Applications`.
2. Double-click **MeetScribe.app** → see the error → click **OK**.
3. Open **System Settings → Privacy & Security**.
4. Scroll down — an **"Open Anyway"** button appears under the block notice.
5. Click **Open Anyway** → confirm. macOS remembers the choice permanently.

**Method 2 — Terminal (most reliable):**

```sh
xattr -cr /Applications/MeetScribe.app
```

Removes the quarantine flag; the app opens normally forever after.

Drop this whole section the moment a Developer ID cert lands and notarization is wired in — at that point Gatekeeper passes silently and this becomes a historical note. Track it against the §7 macOS-launch gating condition.

---

## 6. Feature ideas — what to build, what to refuse, where to track them

### 6.1 Why no "Roadmap" section on the landing page

The maintenance disclosure (§2.9) explicitly says "no roadmap." A roadmap section directly contradicts that — and worse, every item on it becomes an implicit promise. At 1–2 hrs/week of maintenance time, those promises *will* slip, and engineers will notice. Two failure modes to avoid:

- **Vaporware smell.** A roadmap with five "coming soon" items and no shipped releases reads as a side project pretending to be a product.
- **Scope creep by suggestion.** Listing "Slack integration — Q4" on the landing page invites every visitor to ask when it's shipping. Even saying "no" to those requests costs time you don't have.

Better: GitHub issues with an `idea` label, optionally a `IDEAS.md` file in the repo. Engineers know how to read both. The landing page footer links to the filtered issue list. No dates. No commitments. The author can drop in a 👍 reaction or close as `wontfix` without it being a public broken promise.

### 6.2 Cheap features worth considering (low maintenance, high value)

These extend the existing app along axes the architecture already supports — most are a few hours of work each because the adapter / storage / UI patterns are already there.

| Idea | Why it's cheap | Why it's valuable |
|---|---|---|
| **More LLM providers** (Anthropic Claude, Mistral, local Ollama) | The `LLMClientProtocol` adapter pattern already exists; new providers slot in beside DeepSeek / Gemini / OpenAI | Engineers like provider choice. Local Ollama is a strong "fully offline summary" story for the privacy-conscious. |
| **More STT providers** (Deepgram, soniox, etc.) | Same adapter pattern via `StreamingTranscriptionAdapterProtocol` | Hedges against any single STT provider raising prices or shutting down |
| **Export to Markdown / plain text / PDF** | Pure local file generation, no external APIs | Lets users move data into Obsidian / Notion / wiki / git repo without a third-party integration |
| **Custom prompt templates** | Small UI; the prompt is already a single string in `prompts.rs` | Power users will tune for their domain (engineering standup, sales call, lecture notes) — turns one app into ten |
| **Search across past meetings** | SQLite is already there; FTS5 is built into SQLite | Becomes more valuable the longer someone uses the app — natural retention loop |
| **Tags / labels per meeting** | One column in the existing `sessions` table | Cheap organization without folders / hierarchy |
| **Global hotkey to start/stop recording** | Native API on both platforms (`NSEvent.addGlobalMonitorForEvents` / `RegisterHotKey`) | Power-user delight; no engineering risk |
| **Session-level cost meter** | Already advocated in `distribution-strategy.md` §6.7 — track tokens + STT minutes per session | Trust signal: engineers can verify against provider dashboards |

### 6.3 Medium-effort features worth considering

| Idea | Caveat |
|---|---|
| **Speaker diarization** | Both Gladia and AssemblyAI expose this; UI work is the bigger half. Don't build until at least one user asks. |
| **Custom dictionary / glossary for STT** | Both providers support hint terms; significantly improves transcript quality for technical jargon and proper nouns. |
| **Multi-language UI** (separate from transcription language) | Translation files + locale plumbing. Useful for VI users but adds ongoing maintenance per language added. |
| **CLI mode** | "Run a saved meeting through the LLM pipeline from the terminal." Tiny audience but very high signal — exactly the kind of feature engineers respect. |

### 6.4 Features to refuse — say "no" once, link to it

These are the ideas users *will* request. Have a stock answer ready so saying no takes 30 seconds, not 30 minutes. Most are explicitly called out in `distribution-strategy.md` §7 as "narrow scope" violations.

| Idea | Why no |
|---|---|
| **Slack integration** | OAuth surface, API drift, rate limits, every-week breakage. The strategy doc explicitly calls "Notion/Slack/scheduler creep" out as a maintenance trap. Users who want this can pipe the exported Markdown into a Slack workflow themselves. |
| **Notion / Confluence / Obsidian native sync** | Every third-party API is a maintenance tax forever. Markdown export covers 90% of the use case at 1% of the cost. |
| **Calendar integration (Google / Outlook)** | OAuth + scope creep + becomes a sync engine. Massive blast radius for a side project. |
| **Mobile app** | New platform, no shared code, separate stores. Different project entirely. |
| **Cloud sync / team workspace** | Requires a backend. Kills the entire trust pitch. If users want this, they want Granola — say so. |
| **AI agent / "ask questions about your meetings"** | RAG over local meetings is technically interesting but doubles the LLM cost surface and the prompt-quality maintenance burden. Defer until *after* the basics are rock solid. |
| **Auto-join meetings as a bot** | The product literally exists *because* this is the bad option. Never. |

The point of writing this list down is so the response to issue #47 ("can we add Slack?") is "see ROADMAP.md / IDEAS.md — explicitly out of scope, here's why" instead of a fresh paragraph every time.

### 6.5 Where ideas live (recommended structure)

Three lightweight surfaces, no dashboards:

1. **GitHub issues with `idea` / `enhancement` label.** Primary intake. Anyone can file. Author triages monthly.
2. **Pinned issue: "Ideas / wishlist".** One issue with a running checklist linking to the labeled issues. Doubles as a public "what might happen if I have time" list.
3. **`IDEAS.md` in the repo (optional).** Mirror of §6.2/6.3 above with one-line "would consider" / "explicit no" entries. Gets indexed by GitHub search, settles arguments fast.

The landing page footer link "Ideas / wishlist →" can point at any of the three. The pinned issue is probably the right target — it's a single URL that doesn't change, and it's where the conversation actually happens.

---

## 7. Open questions to resolve before launch

These are things to decide once, then stop revisiting.

1. **Domain name.** `meetscribe.app`? `meet-scribe.dev`? Buy something simple and short. Don't bikeshed for a week.
2. **Analytics — yes or no.** Recommended: *no* analytics, or Plausible/GoatCounter at most. If yes, disclose it on the page in plain English.
3. **Email for support.** Use a real personal email or a domain alias (`hi@meetscribe.app`). Don't make people open a GitHub issue for first-touch questions — that's a high bar.
4. **macOS launch date.** What needs to be true before the macOS button stops saying "coming soon"? Pin a date or a gating condition (e.g. "after 50 Windows installs without a crash report") and put it in the §2.9 maintenance disclosure so visitors aren't left guessing.
5. **Newsletter / changelog.** Probably skip. A single-page site with a "blog" of one post looks worse than no blog. If users want macOS-launch notification, a mailto link is enough.
6. **OG / Twitter card image.** One simple image at `/og.png` (1200×630) — app icon + tagline. Generated once, never touched again.

---

## 8. Anti-patterns specifically called out

The landing page should **not**:

- Hide the BYOK requirement until after install
- Use vague phrases like "enterprise-grade encryption" or "AI-powered"
- Promise SLAs, uptime, or support
- Show fake user counts or social proof
- Capture emails before download
- Track users with third-party analytics without disclosure
- Show a chatbot widget
- Auto-play any video or audio
- Use the word "revolutionize"

If something on the page would make a senior engineer roll their eyes, cut it. The audience is engineers. They are paying attention. Reward them for paying attention.

---

## 9. TL;DR for the implementer

- **Who it's for:** privacy-conscious engineers who want a transcription tool that doesn't phone home.
- **Tone:** plain, specific, slightly self-deprecating about being a side project. Never marketing voice.
- **Page structure:** hero → what → why → two-key explainer → cost → how it works → setup → audience-fit → maintenance disclosure → footer.
- **No roadmap section on the page.** Ideas live in GitHub issues with an `idea` label; footer links to a pinned "Ideas / wishlist" issue. See §6.
- **Visual:** single column, system fonts, light/dark, no animations beyond a small flow diagram.
- **Tech:** static HTML or Astro on Cloudflare/GitHub Pages. No SPA. <100KB.
- **Binaries:** GitHub Releases, signed. Windows at launch; macOS button stays "coming soon" until that build is ready.
- **Above all:** make the friction visible above the fold. The two-key requirement is the filter. The page's job is to show it on purpose, not hide it.
