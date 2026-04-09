# ClawBuddy Lite

Real-time OpenClaw agent monitoring dashboard. Built for remote access via Vercel + Tailscale.

## Quick Start

### Deploy to Vercel (2 min)

1. **Create a GitHub repo** (if you don't have one)
   ```bash
   git init
   git add .
   git commit -m "Initial commit: ClawBuddy Lite"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/clawbuddy-lite.git
   git push -u origin main
   ```

2. **Deploy to Vercel**
   - Go to [vercel.com](https://vercel.com)
   - Click "New Project"
   - Import your GitHub repo
   - Click "Deploy"
   - Done. Your dashboard is live.

### Connect to OpenClaw (5 min)

1. **Set up Tailscale on your home laptop**
   - Download [Tailscale](https://tailscale.com/download)
   - Install & sign in
   - Your laptop gets a private IP (e.g., `100.x.x.x`)

2. **Update the gateway URL in your dashboard**
   - Edit `index.html` in your Vercel project
   - Find this line: `const GATEWAY_URL = process.env.REACT_APP_GATEWAY_URL || 'http://127.0.0.1:18789';`
   - Change it to: `const GATEWAY_URL = 'http://YOUR_TAILSCALE_IP:18789';`
   - Push to GitHub (Vercel auto-deploys)

3. **Access from anywhere**
   - Open your Vercel URL
   - You're connected to your home laptop's OpenClaw gateway via Tailscale
   - Fully encrypted, fully private

## Features

- **Dashboard** — Real-time stats, active sessions, token usage
- **Tasks** — Drag-and-drop Kanban board (To Do → Doing → Done)
- **Logs** — Live agent logs with filtering
- **Insights** — Token distribution, session health, analytics
- **Status** — Gateway health, memory state, quick actions

## Environment Variables

```
REACT_APP_GATEWAY_URL=http://your-tailscale-ip:18789
```

If not set, defaults to `http://127.0.0.1:18789` (local only).

## Security

- Your OpenClaw gateway stays on your home laptop (never exposed)
- Tailscale encrypts all traffic between your office and home
- Dashboard is static (no backend secrets stored)
- CORS configured for your gateway only

## Troubleshooting

**"Disconnected" status?**
- Ensure Tailscale is running on your home laptop
- Check that OpenClaw gateway is running: `openclaw status`
- Verify the gateway URL matches your Tailscale IP

**Can't see real data?**
- The dashboard currently uses mock data
- To wire up real API calls, update the `useEffect` hook in `index.html`
- See "Next Steps" below

## Next Steps

1. **Wire real data** — Replace mock data with actual OpenClaw API calls
2. **Add authentication** — Protect your dashboard with API tokens
3. **Automate task sync** — Two-way sync with your OpenClaw task board
4. **Mobile optimization** — Tailor UI for phone viewing

## Built With

- React 18
- Tailwind CSS
- Lucide Icons
- No build step (CDN-based, instant deployment)
