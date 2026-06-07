# Chart Analyzer — sagarkhanal.com/chart-analyzer
## Setup Guide

---

## File Structure
```
your-project/
├── chart-analyzer.html   ← the frontend page
├── server.js             ← backend API proxy
├── package.json
└── .env                  ← your API key (never commit this)
```

---

## Step 1 — Get your Anthropic API key
1. Go to https://console.anthropic.com
2. Create an account → API Keys → Create Key
3. Copy the key (starts with sk-ant-...)

---

## Step 2 — Local testing

```bash
# Install dependencies
npm install

# Create .env file
echo "ANTHROPIC_API_KEY=sk-ant-YOUR_KEY_HERE" > .env

# Start server
npm start
# → Running on http://localhost:3000
```

In `chart-analyzer.html`, the API_URL is already set for self-hosting.
Change line ~270:
```js
const API_URL = 'https://api.anthropic.com/v1/messages';
// Change to:
const API_URL = 'https://sagarkhanal.com/api/analyze';
```

Open `chart-analyzer.html` with VS Code Live Server or just double-click it.

---

## Step 3 — Deploy FREE on Railway (Recommended)

1. Create account at https://railway.app
2. Install Railway CLI or use GitHub:
   - Push this folder to a new GitHub repo
   - New Project → Deploy from GitHub repo
3. Add env variable: `ANTHROPIC_API_KEY` = your key
4. Railway auto-deploys and gives you a URL like:
   `https://sagarkhanal-chart-api.up.railway.app`

---

## Step 4 — Connect to sagarkhanal.com

### Option A: Subdomain (cleanest)
Point `api.sagarkhanal.com` → Railway URL via DNS CNAME

### Option B: Same domain path
If your host supports reverse proxy (Nginx/Apache):
```nginx
location /api/ {
    proxy_pass https://YOUR-RAILWAY-URL.up.railway.app/api/;
}
```

### Option C: Just use Railway URL directly
In `chart-analyzer.html` set:
```js
const API_URL = 'https://YOUR-RAILWAY-URL.up.railway.app/api/analyze';
```

---

## Step 5 — Upload chart-analyzer.html to sagarkhanal.com

Upload `chart-analyzer.html` to your web host in the root folder or
as `/chart-analyzer/index.html` so the URL becomes:
**https://sagarkhanal.com/chart-analyzer**

---

## Cost estimate
- Anthropic API: ~$0.003–0.01 per analysis (very cheap)
- Railway: Free tier available (500 hrs/month)
- Your domain: already have sagarkhanal.com ✓

---

## Summary
| URL | What |
|-----|------|
| sagarkhanal.com/chart-analyzer | The tool page |
| sagarkhanal.com/api/analyze | API endpoint |
