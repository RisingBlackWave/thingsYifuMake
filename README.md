# thingsYifuMake — Deployment Guide

## Project Structure

```
thingsYifuMake/
├── index.html           ← Main site (HTML + CSS + JS engine)
├── projects.json        ← All project content (edit this to add/change projects)
├── .gitignore
├── README.md
└── assets/
    └── projects/
        ├── repairbot-interface/
        │   ├── preview.jpg      ← 440×260 card thumbnail
        │   ├── cover.jpg        ← 1400×600 project page hero
        │   └── loop.mp4         ← optional 5-10s silent video
        ├── tennis-machine-mk1/
        │   └── ...
        └── ...                  ← one folder per project slug
```

## How to edit content

Open `projects.json` in any text editor. Each project looks like:

```json
{
  "mode": "Built",
  "slug": "tennis-machine-mk1",
  "title": "Tennis Ball Machine Mk.1",
  "desc": "A self-commissioned engineering project...",
  "tags": ["Making", "Engineering", "Log"],
  "year": 2024,
  "link": null,
  "previewImage": null,
  "coverImage": null,
  "previewVideo": null
}
```

**To add a real image:**
1. Save your image to `assets/projects/tennis-machine-mk1/preview.jpg`
2. Change `"previewImage": null` → `"previewImage": "assets/projects/tennis-machine-mk1/preview.jpg"`
3. Done. Same pattern for `coverImage` and `previewVideo`.

**To add a new project:**
Add a new object to the JSON array. Create a matching folder in `assets/projects/`.

**To add an external link:**
Set `"link": "https://arxiv.org/abs/..."` — an "open externally ↗" link will appear on the project page.

---

## Local Preview

You need a local server because `fetch()` doesn't work with `file://` URLs.

**Option A — Python (already on your Mac):**
```bash
cd ~/path/to/thingsYifuMake
python3 -m http.server 8000
```
Then open http://localhost:8000

**Option B — Node (if you have it):**
```bash
npx serve .
```

**Option C — VS Code:**
Install the "Live Server" extension → right-click `index.html` → "Open with Live Server"

---

## Deploy to GitHub + Netlify

### Step 1 — Create the GitHub repo

```bash
# Navigate to your project
cd ~/path/to/thingsYifuMake

# Initialise git
git init
git add .
git commit -m "initial constellation"

# Create the repo on GitHub (two ways):

# Option A — GitHub CLI (if installed):
gh repo create thingsYifuMake --public --source=. --push

# Option B — Manual:
# 1. Go to github.com → New Repository → name it "thingsYifuMake"
# 2. Do NOT add README (you already have one)
# 3. Then run:
git remote add origin https://github.com/YOUR_USERNAME/thingsYifuMake.git
git branch -M main
git push -u origin main
```

### Step 2 — Deploy on Netlify (free)

1. Go to [app.netlify.com](https://app.netlify.com) and sign in with GitHub
2. Click **"Add new site"** → **"Import an existing project"**
3. Select your `thingsYifuMake` repo
4. Build settings — leave all fields blank (no build command needed, it's static)
5. Click **Deploy site**

Your site will be live at something like `random-name-123.netlify.app` within 30 seconds.

### Step 3 — Connect your domain

1. In Netlify dashboard → **Domain management** → **Add custom domain**
2. Type `thingsyifumake.com`
3. Netlify will show you DNS records to add

**If you bought the domain on Namecheap / Google Domains / Cloudflare:**
- Go to your domain registrar's DNS settings
- Option A (recommended): Change nameservers to Netlify's (they'll show you the exact values)
- Option B: Add a CNAME record: `www` → `your-site.netlify.app` and an A record pointing to Netlify's IP

4. Netlify auto-provisions HTTPS (free, via Let's Encrypt) — takes ~5 minutes

### Step 4 — Ongoing updates

After any change:
```bash
git add .
git commit -m "added tennis machine photos"
git push
```
Netlify auto-deploys within ~15 seconds. That's it.

---

## Alternative: GitHub Pages (also free)

If you prefer not to use Netlify:

1. Push to GitHub (same as Step 1 above)
2. Go to repo → Settings → Pages
3. Source: "Deploy from a branch" → Branch: `main` → Folder: `/ (root)`
4. Save

Site goes live at `https://YOUR_USERNAME.github.io/thingsYifuMake/`

To connect a custom domain:
1. In repo Settings → Pages → Custom domain → type `thingsyifumake.com`
2. Add these DNS records at your registrar:
   - A records: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - CNAME: `www` → `YOUR_USERNAME.github.io`
3. Check "Enforce HTTPS"

**Netlify vs GitHub Pages:** Netlify is slightly faster, gives you deploy previews, and handles redirects better. GitHub Pages is simpler if you want zero extra accounts. Both are free for static sites.

---

## Domain Registration

If you haven't bought `thingsyifumake.com` yet:

- **Cloudflare Registrar** — cheapest renewals, no markup, good DNS
- **Namecheap** — simple UI, often has first-year deals
- **Google Domains** (now Squarespace Domains) — clean but slightly pricier

A `.com` domain costs ~£8-12/year.

---

## Image Preparation Cheatsheet

| Asset | Dimensions | Format | Max size |
|-------|-----------|--------|----------|
| Preview thumbnail | 440 × 260 px | JPG, 80% quality | ~50 KB |
| Cover hero | 1400 × 600 px | JPG, 85% quality | ~150 KB |
| Video loop | any (16:9 ideal) | MP4 H.264 | < 3 MB |

Quick resize on Mac:
```bash
# Using sips (built into macOS)
sips -z 260 440 input.jpg --out assets/projects/slug/preview.jpg

# Or with ImageMagick (brew install imagemagick)
convert input.jpg -resize 440x260^ -gravity center -extent 440x260 -quality 80 preview.jpg
```

---

## What's Next

Once deployed, priority improvements:
- [ ] Take 5-8 real photos (one per mode minimum)
- [ ] Add year + link data to projects.json
- [ ] Mobile layout pass
- [ ] Making Log as a live chronological section
