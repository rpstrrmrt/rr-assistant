# ⚡ Setup Guide: Fix the Chat Widget — Cloudflare Worker Proxy

Your chat widget isn't working because it needs a **secure backend** to call the Anthropic API. The solution: use **Cloudflare Workers** (free tier, no credit card).

---

## Step 1 — Get Your Anthropic API Key

1. Go to **[console.anthropic.com](https://console.anthropic.com)**
2. Sign in with your Anthropic account
3. Click **API Keys** in the left sidebar
4. Click **Create Key**
5. Give it a name like "RR Assistant"
6. Copy the key and **save it somewhere safe** — you'll need it in a moment
7. **Never share this key publicly**

---

## Step 2 — Create a Cloudflare Worker

1. Go to **[workers.cloudflare.com](https://workers.cloudflare.com)**
2. Click **Sign Up** (it's free, no credit card required)
3. Verify your email
4. Click **Create a Service** or **Create Application**
5. Choose **Create a Worker** (not a full application)
6. You'll see a code editor — delete all the code
7. Paste the entire code from `cloudflare-worker.js` (the file I created for you)
8. Click **Save and Deploy** at the top right
9. You'll see a URL like: `https://rr-assistant-abc123.YOUR_ACCOUNT.workers.dev`
   - **Copy this URL** — you'll need it next

---

## Step 3 — Add Your API Key to the Worker

1. From the Worker page, click **Settings** (top menu)
2. On the left, click **Variables**
3. Under **Environment Variables**, click **Add Variable**
4. **Variable name:** `ANTHROPIC_API_KEY`
5. **Value:** Paste your API key from Step 1
6. Click **Encrypt** (checkbox)
7. Click **Save**
8. Click **Deploy** to apply the changes

---

## Step 4 — Update Your HTML File

1. Open `index.html` (the chat widget file)
2. Find this line (should be around line 400–420):
   ```javascript
   const WORKER_URL = 'https://rr-assistant.YOUR_CLOUDFLARE_ACCOUNT.workers.dev';
   ```
3. Replace `YOUR_CLOUDFLARE_ACCOUNT` with your actual Cloudflare account subdomain
   - Example: if your Worker URL is `https://rr-assistant-abc123.myaccount.workers.dev`, replace it with that full URL
4. Save the file
5. Upload it back to GitHub (same process as before — edit file in GitHub, commit)

---

## Step 5 — Test It

1. Wait 2–3 minutes for GitHub to update
2. Go to your GitHub Pages URL: `https://rpstrrmrt.github.io/rr-assistant/`
3. Type a message in the chat
4. **The assistant should now respond!**

---

## Troubleshooting

**"API connection failed" error:**
- Double-check your WORKER_URL is correct in the HTML
- Verify your Anthropic API key was added to the Worker (Settings → Variables)
- Make sure the key is marked as **Encrypted**
- Wait 5 minutes and try again

**Worker won't deploy:**
- Make sure you pasted the entire `cloudflare-worker.js` code
- Check for syntax errors (missing brackets, quotes)
- Click **Deploy** again

**Still not working:**
- Open your browser's Developer Tools (F12 or right-click → Inspect)
- Go to the **Console** tab
- Try sending a message
- Look for error messages and share them with me

---

## Your Worker URL (for reference)

Once you create your Worker, it will look like:
```
https://rr-assistant-XXXXXX.YOUR_ACCOUNT.workers.dev
```

This is what goes in the HTML file's `WORKER_URL` variable.

---

## Security Notes

✅ Your API key is **secure** — it lives on Cloudflare servers only
✅ The Worker encrypts it and never exposes it to the browser
✅ All requests go through the Worker proxy, not directly to Anthropic
✅ Free tier: 100,000 requests/day (plenty for your needs)

---

Done! Your chat widget should now be fully functional. 🎖️
