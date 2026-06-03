# Deploying tfernandes.com

## What this repo contains

A static HTML/CSS site. There is no package manager, dependency install, or build step.

```
site/
├── index.html
├── CNAME
└── avatar.jpg
```

## GitHub repository

This site is intended to live at:

- Repository: `TiagoRMFernandes/tfernandes.com`
- Production branch: `main`
- Site root / output directory: `/`

If setting up the repo from this folder locally:

```sh
cd ~/Downloads/site
git init
git add .
git commit -m "Launch personal site"
git branch -M main
git remote add origin https://github.com/TiagoRMFernandes/tfernandes.com.git
git push -u origin main
```

## Option A — Cloudflare Pages

Use this if Cloudflare will host the site from GitHub.

1. In Cloudflare, go to **Workers & Pages**.
2. Create a Pages project by importing the GitHub repo `TiagoRMFernandes/tfernandes.com`.
3. Use these build settings:
   - Production branch: `main`
   - Build command: `exit 0`
   - Build output directory: `/`
4. Deploy once.
5. Open the Pages project, go to **Custom domains**, and add `tfernandes.com`.

Cloudflare will create the needed DNS record automatically when the zone is already on Cloudflare.

## Option B — GitHub Pages with Cloudflare DNS

Use this if GitHub Pages will host the site and Cloudflare will only manage DNS.

1. In GitHub, open `TiagoRMFernandes/tfernandes.com` → **Settings** → **Pages**.
2. Set **Source** to **Deploy from a branch**.
3. Set branch to `main` and folder to `/ (root)`.
4. Set the custom domain to `tfernandes.com`.
5. In Cloudflare DNS, remove conflicting root-domain records and add:

   | Type | Name | Content |
   | ---- | ---- | ------- |
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |
   | CNAME | www | TiagoRMFernandes.github.io |

6. Leave those Cloudflare records as **DNS only** while GitHub provisions HTTPS.
7. Back in GitHub Pages, enable **Enforce HTTPS** once GitHub allows it.

DNS changes can take up to 24 hours to propagate, although they often settle much faster.

## Adding Posts

1. Create a `posts/` folder if it does not exist.
2. Add a new post file using kebab-case, for example `posts/my-new-post.html`.
3. Add a new `<a class="post-item">` block in `index.html` linking to it.
4. Commit and push. GitHub Pages or Cloudflare Pages will redeploy from `main`.

## Updating The Photo

Drop your headshot into the `site/` folder as `avatar.jpg`, commit, and push.
