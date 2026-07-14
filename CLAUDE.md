# CLAUDE.md — tracethechicagotaste.com

Personal brand site for @tracethechicagotaste, a Chicago food TikTok account. Owner: Trace (GitHub: mcgarrymurr). Voice: dry, confident, understated humor. Tagline: "tracing Chicago's food scene with questionable commentary."

## Architecture

Static site, no build step, no framework. Plain HTML/CSS/JS, one file per page.

- `index.html` — currently the full-featured v1 (hero, video grid, recommendation engine, blog, contact)
- `logo.svg` — brand badge (circular illustration; character with Chicago foods). Referenced by pages, do not inline it.
- `favicon-32.png`, `apple-touch-icon.png`, `icon-512.png` — generated from logo.svg
- Restaurant data lives in a `SPOTS` JavaScript array at the bottom of the page that uses it. Filter chips auto-generate from the data. To add a restaurant, edit only that array.

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

## Current state & agreed next step (v2)

A minimal landing page was designed and approved (see `minimal.html` in the handoff, or ask Trace for it): centered logo at 340px, lowercase `@tracethechicagotaste` in red linking to TikTok, tagline, vertical text links (Instagram, TikTok, Contact), Contact opens a native `<dialog>` with trace@ email + Instagram DM link.

Agreed architecture for v2 (owner confirmed direction, not yet committed):
- `/` (index.html) → the minimal landing page
- `/eat` (eat.html) → the current full site (recommendation engine, videos, blog), linked from the landing page
- Do NOT create separate mobile/desktop sites — owner floated this twice; the agreed approach is the page split above. Everything must stay responsive.

## Open items

1. Instagram URL is unverified — https://www.instagram.com/tracethechicagotaste is a guess. Confirm handle with Trace before shipping.
2. All restaurant entries in `SPOTS` are placeholders; real data to come (possibly from Trace's Beli ratings — Beli has no public API, manual entry likely).
3. Video cards link to the TikTok profile generically; swap for real video URLs or TikTok embeds.
4. Blog posts are placeholder titles.
5. Verify DKIM/DMARC TXT records made it to Cloudflare (see DNS section).
6. Gmail send-as for trace@ not yet configured.

## Conventions

- Commit messages: short version-style summaries, e.g. `v2 — minimal landing + /eat split`.
- Keep pages self-contained (styles and scripts in the HTML file). No build tooling unless the project genuinely outgrows it.
- Test on mobile width before committing; TikTok traffic is mobile-heavy.
