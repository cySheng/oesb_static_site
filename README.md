# Optimus Engineering — static site

Plain HTML/CSS, no build step. Everything served lives in `public/`.

```
public/
  index.html     homepage (responsive: desktop / tablet / mobile)
  404.html
  styles.css
  fonts/         self-hosted Barlow Condensed, IBM Plex Sans, IBM Plex Mono (latin)
  favicon.svg
  _headers       Cloudflare Pages response headers
  robots.txt
```

## Before going live

Replace placeholders in `public/index.html`:

- `[YOUR-EMAIL]` (mailto links) and `[YOUR EMAIL]` (displayed address)
- `[OFFICE ADDRESS]` (footer)

## Images

Originals (PNG) live in `assets-src/images/` — not deployed. Web versions (WebP) live in `public/images/`.
Gallery tiles are fixed shapes and crop photos to fit, so source sizes don't need to match.
To add or replace a photo, put the original in `assets-src/images/` and convert:

```bash
magick assets-src/images/my_photo.png -resize '1600x>' -strip -quality 82 public/images/my-photo.webp
```

Images are cached for 7 days (`_headers`); use a new filename if you replace a photo and need it to show immediately.

## Preview locally

```bash
npx serve public
```

## Deploy — Cloudflare Workers (static assets)

`wrangler.toml` serves `public/` as static assets; no Worker script.

**Git integration (auto-deploy on push):** Cloudflare dashboard → Workers & Pages → Create → Import a repository.
Build command: *(none)* · Deploy command: `npx wrangler deploy`.
The Worker name in the dashboard must match `name` in `wrangler.toml`.

**Manual deploy:**

```bash
npx wrangler deploy
```

Custom domain: Worker → Settings → Domains & Routes → add domain.
