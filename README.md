# tracethechicagotaste.com

Personal site for [@tracethechicagotaste](https://www.tiktok.com/@tracethechicagotaste) — Chicago food reviews, videos, recommendations, and business inquiries.

## Files

| File | Purpose |
|---|---|
| `index.html` | Minimal landing page — logo, handle, tagline, and links out |
| `eat.html` | "Where to Eat" placeholder — the recommendation engine is still being designed |
| `blog.html` | The blog — longer-form posts |
| `logo.svg` | Brand badge, used in nav + hero |
| `favicon-32.png` / `apple-touch-icon.png` / `icon-512.png` | Favicons, generated from the logo |

## Editing content

**Blog posts** — the post list in `blog.html`. Each post is one `<a class="post">` block.

**Restaurants / videos** — not live yet. The old full site (recommendation engine + video grid + `SPOTS` array) is still in git history if you want to reference or resurrect it — see the commit before `eat.html` became a placeholder.

**Colors** — all in the `:root` CSS variables at the top, pulled from the logo (`--red: #e5002b`, `--sky: #42b5e8`, `--ink: #0d2d5f`).

## Deploying

Hosted on Cloudflare Pages, connected to this repo. Every commit to `main` auto-deploys. No build step — framework preset "None", output directory `/`.
