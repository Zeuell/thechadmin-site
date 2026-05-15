# thechadmin.com

Personal site for Chad Dodson — Cisco Technical Consulting Engineer, AI / Agentic Engineering.

Deployed via **Cloudflare Pages** at <https://thechadmin.com>.

## Stack

Vanilla static site — no build step.

- `index.html` — single-page resume site
- `styles.css` — navy / amber / cream theme that carries through from the printed resume
- `assets/`
  - `paper.png` — cream paper texture (background)
  - `badge.png` — AI / Agentic / MCP / AITECH circular badge
  - `Chad_Dodson_Resume.pdf` — downloadable printed-resume PDF

## Deploy

Cloudflare Pages builds on push to `main`. There is no build command — Cloudflare serves the repo root as the static site.

To deploy manually from the command line:

```powershell
npx wrangler pages deploy . --project-name thechadmin
```

## Local preview

Open `index.html` directly in the browser, or run any static server:

```powershell
python -m http.server 8080
```

Then visit <http://localhost:8080>.

## Updating content

Edit `index.html` and push to `main`. Cloudflare Pages will rebuild and roll the new version out automatically (~30 seconds).
