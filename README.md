# tracethechicagotaste.com

Personal site for [@tracethechicagotaste](https://www.tiktok.com/@tracethechicagotaste) — Chicago food reviews, videos, recommendations, and business inquiries.

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire site — markup, styles, and scripts in one file |
| `logo.svg` | Brand badge, used in nav + hero |
| `favicon-32.png` / `apple-touch-icon.png` / `icon-512.png` | Favicons, generated from the logo |

## Editing content

**Restaurants** — everything in the "Where to Eat" section is driven by the `SPOTS` array near the bottom of `index.html`. Add or edit entries there; filter chips generate automatically from whatever neighborhoods and cuisines appear in the data. Ratings are 1–4 (the Chicago scale).

**Videos** — cards in the `#videos` section. Swap the `href` for real TikTok video URLs, or replace a card with TikTok's native embed code (Share → Embed on any video).

**Blog posts** — the `#blog` section post list. Each post is one `<a class="post">` block.

**Colors** — all in the `:root` CSS variables at the top, pulled from the logo (`--red: #e5002b`, `--sky: #42b5e8`, `--ink: #0d2d5f`).

## Deploying

Hosted on Cloudflare Pages, connected to this repo. Every commit to `main` auto-deploys. No build step — framework preset "None", output directory `/`.
