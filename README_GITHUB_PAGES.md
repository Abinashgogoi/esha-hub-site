# ESHA Hub Site — GitHub Pages Setup

This folder is ready to push to a new GitHub repo and deploy with **GitHub Pages**.

## 1) Create a repo and push

```bash
# create a new repo on GitHub first, e.g. github.com/your-user/esha-hub-site
cd esha_hub_github_ready
git init -b main
git add .
git commit -m "Publish ESHA Hub site v2"
git remote add origin https://github.com/YOUR-USER/esha-hub-site.git
git push -u origin main
```

The included workflow `.github/workflows/deploy.yml` will publish the site automatically to **Pages**.

## 2) Enable Pages (first time only)

On GitHub → **Settings → Pages**:
- Source: **GitHub Actions** (already configured by workflow)

## 3) Custom domain (Zoho-managed DNS)

Edit the `CNAME` file in the repo root to your domain or subdomain, e.g.

```
esha-hub.example.in
```

Then in **Zoho Domains / Zoho DNS** add records:

### If using a subdomain (e.g., `www.esha-hub.in` or `esha-hub.example.in`)
Create a **CNAME** record:
- **Host/Name:** `www` (or `esha-hub` if you want `esha-hub.example.in`)
- **Target/Value:** `YOUR-USER.github.io.`
- **TTL:** default

### If using the apex/root domain (e.g., `esha-hub.in`)
Create **A records** pointing to GitHub Pages:
- `185.199.108.153`
- `185.199.109.153`
- `185.199.110.153`
- `185.199.111.153`

(If Zoho supports **ALIAS/ANAME** for root, you can alternatively point root to `YOUR-USER.github.io` with that.)

> After DNS propagates, GitHub Pages will issue HTTPS automatically. In GitHub → Settings → Pages, set the Custom domain and check **Enforce HTTPS**.

## 4) Notes for your site

- Path with spaces such as `esha hub About/` is fine, but be careful when linking. The current join page uses:
  ```js
  const ABOUT_URL = "../esha hub About/About.html";
  ```
  This works with relative links on Pages. If you later move files, update this constant accordingly.

- The site includes `.nojekyll` so folders like `assets` will be served without Jekyll processing.

- No build step is required; this is a plain static site. Just commit HTML/CSS/JS/images.

## 5) Update flow

- Edit your files locally, test, then:

```bash
git add -A
git commit -m "Update content"
git push
```

The workflow will redeploy automatically.
