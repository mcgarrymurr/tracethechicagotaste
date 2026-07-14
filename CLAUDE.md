# CLAUDE.md — tracethechicagotaste.com

Personal brand site for @tracethechicagotaste, a Chicago food TikTok account. Owner: Trace (GitHub: mcgarrymurr). Voice: dry, confident, understated humor. Tagline: "tracing Chicago's food scene with questionable commentary."

## Architecture

Static site, no build step, no framework. Plain HTML/CSS/JS, one file per page.

- `index.html` — the minimal landing page (v2, live). Logo, handle, tagline, links to Instagram/TikTok/`/eat`/`/blog`/Contact. Contact opens a native `<dialog>`.
- `eat.html` — "Where to Eat" placeholder ("coming soon"). The full recommendation-engine build (hero, video grid, `SPOTS` array, filter chips, blog section, work-with-me contact) is intentionally on hold while Trace thinks through the design more; the old full-site version is preserved in git history (see commits before the `eat.html` rewrite) rather than deleted.
- `blog.html` — the blog. Longer-form post list (currently placeholder titles), pulled out of the old `eat.html` when it became a placeholder.
- `logo.svg` — brand badge (circular illustration; character with Chicago foods). Referenced by pages, do not inline it.
- `favicon-32.png`, `apple-touch-icon.png`, `icon-512.png` — generated from logo.svg

## Deployment — IMPORTANT

- Deployed as a **Cloudflare Worker** (static assets), NOT Cloudflare Pages. Project name `tracethechicagotaste` on account mcgarrymurr@gmail.com. Do not follow Pages-specific docs; Workers custom-domain behavior differs (hostnames must be claimed in Worker → Domains, plain CNAMEs are not sufficient).
- Auto-deploys from `main` on every push. No CI config needed.
- Live at https://tracethechicagotaste.com and https://www.tracethechicagotaste.com (both attached as Worker custom domains). Worker URL: tracethechicagotaste.mcgarrymurr.workers.dev
- DNS is on Cloudflare (nameservers migrated from Porkbun July 2026).

## DNS / Email — DO NOT BREAK

Email is Porkbun hosted email; DNS records that must never be deleted or modified in Cloudflare:
- MX `@` → fwd1.porkbun.com (priority 10) and fwd2.porkbun.com (priority 20)
- TXT `@` → `v=spf1 include:_spf.porkbun.com ~all`
- Possibly TXT `default._domainkey` and `_dmarc` (DKIM/DMARC — may still need copying from Porkbun's panel; verify)

Business email: trace@tracethechicagotaste.com (Porkbun hosted; Gmail send-as setup pending — SMTP smtp.porkbun.com:587 STARTTLS, POP pop.porkbun.com:995 SSL).

## Brand system

- Palette (extracted from logo.svg — use these exact values): red `#e5002b`, sky blue `#42b5e8`, navy ink `#0d2d5f`, white dominant. Cream whisper `#fdfaf2` for alternate section backgrounds.
- Type: Barlow (body) + Barlow Condensed (display, uppercase) from Google Fonts.
- Signature motif: six-pointed Chicago municipal star (SVG symbol id `chi-star` exists in both page drafts). Ratings are **out of 4 stars, like the Chicago flag** — never 5.
- Design direction: clean, bright, white-dominant, minimal. Owner consistently pushed toward less.

## Writing style for site copy

Plain verbs, no marketing-speak. Banned: delve, seamless, robust, unlock, unleash, empower, elevate, leverage, game-changer, journey, landscape, holistic, cutting-edge. No em dashes in site copy — use commas, periods, or colons. Dry humor over enthusiasm. Example of the register: "It's a two. It knows what it did."

## Current state (v2 — live)

v2 shipped: minimal landing at `/`, full old site split to `/eat`. `/eat` was then further reduced to a "coming soon" placeholder, and its blog section split out into its own `/blog` page, since Trace wants to think through the recommendation engine more before building it out.

Do NOT create separate mobile/desktop sites — owner floated this twice; the agreed approach is the page split above. Everything must stay responsive.

## Open items

1. Instagram URL is unverified — https://www.instagram.com/tracethechicagotaste is a guess. Confirm handle with Trace before shipping.
2. The recommendation engine (`SPOTS` array, filter chips, restaurant cards) is on hold — Trace wants to think through the design more. Previous full build is in git history if resurrecting it.
3. Video grid and "work with me" business contact section were dropped when `/eat` became a placeholder — no current home for them; revisit if/when needed.
4. Blog posts in `blog.html` are placeholder titles.
5. Verify DKIM/DMARC TXT records made it to Cloudflare (see DNS section).
6. Gmail send-as for trace@ not yet configured.

## Conventions

- Commit messages: short version-style summaries, e.g. `v2 — minimal landing + /eat split`.
- Keep pages self-contained (styles and scripts in the HTML file). No build tooling unless the project genuinely outgrows it.
- Test on mobile width before committing; TikTok traffic is mobile-heavy.
