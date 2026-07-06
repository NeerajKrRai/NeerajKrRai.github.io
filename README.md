# Neeksha's Apps — hub for `apps.neeksha.com`

This repo (`NeerajKrRai/NeerajKrRai.github.io`) is Neeraj's GitHub **user site**.
It serves the landing page at **https://apps.neeksha.com** and owns the custom
domain for every app beneath it.

> **New session? Start here.** This README is the source of truth for how the
> `apps.neeksha.com` family is wired and how to add another app. Read it before
> touching DNS, Pages, or `index.html`.

## ⚠️ Don't repurpose this repo — it's the one-and-only user-site slot

`NeerajKrRai.github.io` is the account's **user site** (GitHub gives you exactly
one). It's special for a reason we depend on: a custom domain attached here
(`apps.neeksha.com`) automatically serves the root **and** every other repo as
a subpath (`apps.neeksha.com/summer-bar/`). That auto-nesting is the entire
reason "add an app = new repo + a card here" works. **Keep this repo as the
apps hub. Do not convert it into a personal homepage or a single app.**

Intended account layout (keep it this way):

| Purpose | Repo | URL |
|---|---|---|
| Kids' apps hub (this repo) | `NeerajKrRai.github.io` (user site) | `apps.neeksha.com` + `/‹app›/` |
| Neeraj's personal site | `neeraj-personal-site` (project site) | its own custom domain, served at that domain's root |

A user site and a project site can each carry their own custom domain, so the
personal site and the apps hub coexist with zero conflict — they just use
different domains. The only thing "spent" is the bare `neerajkrrai.github.io/`
vanity root, which is moot when custom domains are in use.

## How the hosting works

- **This repo** = the hub. Its `index.html` is the landing page ("Neeksha's
  Apps") and its `CNAME` file (`apps.neeksha.com`) is what attaches the domain.
  **The domain lives here and nowhere else.**
- **Each app = its own repo.** A GitHub Pages project site is automatically
  served at `apps.neeksha.com/<repo-name>/`. Example: repo `summer-bar` →
  https://apps.neeksha.com/summer-bar/ (that's Neeksha's Summer Refreshment
  Bar; source at github.com/NeerajKrRai/summer-bar, deployed from its
  `gh-pages` branch, `.nojekyll` required).
- **DNS/TLS** (Cloudflare zone `neeksha.com`): a single **CNAME `apps →
  neerajkrrai.github.io`**, proxied (orange), SSL mode **"Full"** + Always Use
  HTTPS. TLS is Cloudflare's edge cert. Do **not** set "Full (strict)" while
  proxied — GitHub can't mint its own cert behind the proxy (flip the record
  grey for an hour if strict is ever needed). Security already applied on the
  zone: HSTS, min TLS 1.2, SPF/DMARC/DKIM reject-all, response headers
  (X-Frame-Options DENY, nosniff, Referrer-Policy).

## Adding a new app — checklist

1. **Build the app** as a static site (its own repo, folder `www/` or root —
   plain HTML/CSS/JS works; no build step needed).
2. **Create the repo** and deploy it to GitHub Pages:
   - Repo name becomes the URL path, so pick it deliberately
     (`coloring-book` → `apps.neeksha.com/coloring-book/`). Lowercase, hyphens.
   - Put the site on a `gh-pages` branch (or `main` root) and enable Pages for
     that branch. Add an empty **`.nojekyll`** file so files with leading
     underscores/dots serve raw.
   - **Do NOT add a `CNAME` file to the app repo.** The domain belongs to this
     hub repo only; a CNAME in an app repo would fight for the domain.
   - It's now live at `https://apps.neeksha.com/<repo-name>/` (give Pages a
     minute to build).
3. **Add a card to this hub's `index.html`** — copy the block below, replacing
   the placeholder `.soon` card (or adding alongside it). Use the app's own
   192px icon path.
4. **Commit + push this repo.** The landing page updates within a minute.

### Card template (paste into the `.grid` div in `index.html`)

```html
<a class="card" href="/REPO-NAME/">
  <img src="/REPO-NAME/icons/icon-192.png" alt="APP NAME icon">
  <div>
    <div class="t">APP NAME</div>
    <div class="d">One-line kid-friendly description ✨</div>
  </div>
  <div class="go">→</div>
</a>
```

The existing `.soon` "Something new… brewing!" card is a placeholder — replace
it with a real card when the next app ships, or leave one in as a teaser.

## Design language (keep it consistent across apps)

Kawaii/anime, kaomoji (`♪( ´∀｀)` `人(´∀｀ )♪`), soft palette — rosy charcoal
`#2B2B2B`, royal green `#2D6A4F`/`#52B788`, dusty rose `#C97B84`; fonts Playfair
Display + DM Sans (self-hosted in `fonts/`, no external requests). Every app is
**age-appropriate (Neeksha is 8), make-believe, no ads, no tracking.**

---
*Built with love — ♪( ´∀｀)人(´∀｀ )♪ ～♥*
