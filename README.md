# hoosiermacadmins-org

Static site for [Hoosier Mac Admins](https://www.hoosiermacadmins.org), migrated off Google Sites. Plain HTML/CSS/JS — no build step, no framework.

## Structure

```
/
├── index.html               Home
├── about.html                About
├── calendar.html              Calendar (Google Calendar embed)
├── hosting.html                Host a meetup (Google Form embed)
├── speaking.html               Speak at a meetup (Google Form embed)
├── code-of-conduct.html        Code of Conduct
├── past-meetings/
│   ├── index.html               Past Meetings list
│   └── february-2024.html       February 2024 recap
├── 404.html                    Custom not-found page
├── assets/
│   ├── css/styles.css           Shared stylesheet (Indiana navy & gold theme)
│   ├── js/main.js               Mobile nav toggle, footer year
│   └── img/favicon.svg
├── _headers                    Cloudflare Pages response headers
├── robots.txt
└── sitemap.xml
```

Every page shares the same header/nav and footer markup (hand-duplicated, since this is a static, no-build site). All internal links and asset references use root-relative paths (e.g. `/about`, `/assets/css/styles.css`), so the site works correctly however deep a page sits in the folder structure.

## Local preview

No build tools needed — any static file server works:

```bash
cd /path/to/hoosiermacadmins-org
python3 -m http.server 8080
# visit http://localhost:8080
```

## Deploying with Cloudflare Pages (connected to GitHub)

1. Push this repo to GitHub (`hoosiermacadmins/hoosiermacadmins-org`).
2. In the [Cloudflare dashboard](https://dash.cloudflare.com/), go to **Workers & Pages → Create → Pages → Connect to Git**.
3. Select the `hoosiermacadmins/hoosiermacadmins-org` repository.
4. Build settings:
   - **Framework preset:** None
   - **Build command:** *(leave blank)*
   - **Build output directory:** `/`
5. Deploy. Cloudflare will build a `*.pages.dev` preview URL immediately.
6. Go to the Pages project → **Custom domains** → add `hoosiermacadmins.org` and `www.hoosiermacadmins.org`. If the domain's DNS is already on Cloudflare, this is one click; Cloudflare adds the needed CNAME/DNS records automatically.
7. Every push to `main` auto-deploys; pushes to other branches get their own preview URL.

No `wrangler.toml` or CI config is required for a plain static site — Cloudflare Pages builds directly from the repo.

## Updating content

- **New event or news item on the homepage:** edit the "Latest news" card grid in `index.html`.
- **New past meeting:** add a `.timeline-item` entry in `past-meetings/index.html`, and create a new page under `past-meetings/` following the pattern in `february-2024.html`.
- **Code of Conduct / About text:** edit directly in `code-of-conduct.html` / `about.html` — plain HTML, no templating.
