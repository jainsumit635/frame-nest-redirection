# GitHub Pages Dynamic Cloudflare Redirection Setup

This guide explains how to publish the static redirect page located in `docs/` to **GitHub Pages** so visitors to your GitHub Page are automatically routed to your dynamic Cloudflare tunnel instance.

---

## 🚀 How It Works

1. Visitors navigate to your permanent GitHub Pages URL:
   `https://<your-username>.github.io/<repo-name>/`
2. The page fetches [`docs/current-tunnel.json`](file:///Users/sumit/Documents/Development/frame-nest/docs/current-tunnel.json) (or reads query params / browser storage).
3. The page displays a sleek connecting screen and instantly redirects the browser to the live Cloudflare Tunnel URL.

---

## 🛠️ Step 1: Enable GitHub Pages in your Repository

1. Push your repository changes to GitHub (`git add docs/ && git commit -m "Add GitHub Pages redirect" && git push`).
2. Go to your repository on **GitHub.com**.
3. Click on **Settings** (top navigation tab).
4. In the left sidebar under *Code and automation*, click **Pages**.
5. Under **Build and deployment**:
   - **Source**: Select `Deploy from a branch`.
   - **Branch**: Select `main` (or `master`) and change the folder dropdown from `/ (root)` to `/docs`.
   - Click **Save**.
6. GitHub Pages will build and deploy your site within 1–2 minutes. Your live page URL will appear at the top (e.g. `https://<username>.github.io/frame-nest/`).

---

## 🔄 Step 2: Updating the Live Tunnel URL

When you restart your server or launch a new Cloudflare Quick Tunnel (`cloudflared`), you have 3 easy ways to direct users:

### Option A: Auto-update `current-tunnel.json` (Recommended for repo updates)
Whenever you start your tunnel and get a new URL (e.g. `https://xyz.trycloudflare.com`):
1. Update [`docs/current-tunnel.json`](file:///Users/sumit/Documents/Development/frame-nest/docs/current-tunnel.json):
   ```json
   {
     "url": "https://xyz.trycloudflare.com",
     "updated_at": "2026-10-10T19:50:00Z"
   }
   ```
2. Commit and push:
   ```bash
   git add docs/current-tunnel.json
   git commit -m "Update live tunnel URL"
   git push
   ```

### Option B: Query Parameter Link
Share your GitHub Pages URL with the tunnel URL appended:
`https://<username>.github.io/frame-nest/?url=https://xyz.trycloudflare.com`

The page will immediately redirect and save the target into browser memory.

### Option C: In-Page Quick Config
Opening the GitHub Page without a dynamic JSON endpoint lets you click **"Need to update or manually enter tunnel URL?"**, paste your new URL once, and click **Save & Go**.
