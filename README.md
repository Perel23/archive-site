# ARCHIVE — Deployment Guide

## What's in this folder

```
archive-site/
├── index.html          ← The website
├── tracks.json         ← All your track/artist data (the CMS)
├── netlify.toml        ← Netlify configuration
├── media/              ← Drop your audio + visual files here
│   ├── my-song.mp3
│   └── my-visual.jpg
└── admin/
    ├── index.html      ← Netlify CMS web UI
    └── config.yml      ← CMS field configuration
```

---

## Step 1 — Push to GitHub

```bash
cd archive-site
git init
git add .
git commit -m "initial archive"
gh repo create archive-site --public --push --source=.
```
(If you don't have the `gh` CLI: create a repo on github.com and follow their push instructions.)

---

## Step 2 — Deploy on Netlify (free)

1. Go to **https://app.netlify.com** → "Add new site" → "Import an existing project"
2. Connect GitHub, select your `archive-site` repo
3. Build settings: leave everything blank (no build command needed)
4. Click **Deploy site**
5. Your site is live at `https://[random-name].netlify.app` in ~30 seconds

---

## Step 3 — Enable the CMS (so you can add tracks from a web form)

### 3a. Enable Netlify Identity
In your Netlify dashboard → **Identity** tab → click **Enable Identity**

### 3b. Enable Git Gateway
In Identity settings → **Services** → **Git Gateway** → Enable it

### 3c. Create your admin account
- Go to `https://your-site.netlify.app/admin/`
- Click "Sign up" — enter your email
- Check your email for the confirmation link
- You're in! You'll see the CMS dashboard.

---

## Step 4 — Adding a new track

### Option A: Via the CMS (no coding)
1. Go to `your-site.netlify.app/admin/`
2. Click **Tracks** → **All Tracks**
3. Scroll to the bottom of the list → click **Add Tracks item**
4. Fill in: Title, Genre, Year, Description, upload your Audio and Visual files, add Collaborators
5. Click **Publish** — the site updates automatically within 1-2 minutes

### Option B: Edit tracks.json directly
Add a new object to the array:
```json
{
  "id": 5,
  "title": "Your Song Title",
  "titleItalic": "Song",
  "genre": "Your Genre",
  "year": "2025",
  "description": "Your description here.",
  "audioSrc": "media/your-file.mp3",
  "visualSrc": "media/your-visual.jpg",
  "visualType": "image",
  "accentColor": "#c8b86e",
  "bgGradient": "linear-gradient(135deg, #1a1208 0%, #1a0f0f 100%)",
  "collaborators": [
    { "name": "Artist Name", "role": "Visual Art" },
    { "name": "Another Name", "role": "Mixing" }
  ]
}
```
Commit and push → Netlify redeploys automatically.

---

## Adding media files

Put audio/visual files in the `media/` folder before deploying, or upload them through the CMS.

**Supported formats:**
- Audio: `.mp3`, `.wav`, `.flac`, `.ogg`
- Visuals: `.jpg`, `.png`, `.gif`, `.mp4`, `.webm`

**File size tips:**
- Compress MP3s to 192kbps for fast loading
- Resize images to max 1920px wide
- Keep video files under 20MB (or use a YouTube/Vimeo embed)

---

## Custom domain (when you're ready)

Netlify dashboard → **Domain settings** → **Add custom domain**
Enter your domain (bought from Namecheap, GoDaddy, etc.) and follow the DNS instructions.
HTTPS is automatic and free via Let's Encrypt.

---

## Customising the site

| What | Where |
|------|-------|
| Your name / site title | `index.html` → search "ARCHIVE" |
| Social links | `index.html` → `<footer>` section |
| Hero text | `index.html` → `.hero` section |
| Fonts / colors | `index.html` → `:root` CSS variables |
| Track data | `tracks.json` |
