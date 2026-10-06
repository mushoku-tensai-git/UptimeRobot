# UptimePulse

> A lightweight, self-contained uptime monitoring dashboard and public status page with an editorial developer interface.

---

## Overview

UptimePulse is an open-source, client-side uptime monitoring dashboard inspired by UptimeRobot and styled with the Resend editorial design system. It allows developers to monitor HTTP(S) endpoints, configure heartbeat checks for cron jobs, generate embeddable status badges, preview multi-region edge latency, and broadcast incident updates without running a dedicated database or backend server.

---

## Features

- **Multi-Protocol Monitoring**:
  - `HTTP / HTTPS`: Monitors web apps, landing pages, and REST APIs with configurable status codes and keyword assertions.
  - `Heartbeat / Push`: Generates unique ping tokens for background jobs, crontabs, and worker scripts.
  - `API Endpoint`: Supports custom request headers (e.g., `Authorization: Bearer <token>`).
- **Real Probing Engine**: Dual-fallback probe mechanism combining direct `fetch` calls, CORS proxies, and image-based beacon fallbacks to measure round-trip network latency.
- **Global Edge Latency (Geo-Ping)**: Telemetry inspector with simulated multi-region latency distribution (US East, EU Central, Asia South, AP East).
- **Embeddable Integrations**:
  - **Live SVG Status Badges**: Copy-paste badges for GitHub `README.md`, personal portfolios, and docs.
  - **1-Line Floating Widget**: Drop-in JavaScript widget to show real-time uptime status on any website.
- **Alerts & Incident Management**:
  - Discord and Slack webhook outage notifications.
  - In-browser synthesized audio alerts powered by Tone.js.
  - Automatic incident tracking with root-cause logging and duration calculation.
- **Operations & Reporting**:
  - **Scheduled Maintenance Mode**: Suppress false alarms during planned migrations and deployments.
  - **SLA Telemetry Export**: Download historical 30-day uptime and latency audit logs as CSV or JSON.
  - **Public Status Page**: One-click toggle to present a clean, read-only status page with custom operational announcements.
- **Zero-Backend Architecture**: Runs completely in the browser with fault-tolerant local state persistence.

---

## Tech Stack

| Layer | Technology |
|---|---|
| **Core** | HTML5, Vanilla JavaScript (ES6+), CSS3 |
| **Styling** | Tailwind CSS (CDN), Custom Editorial Design Tokens |
| **Typography** | Editorial Serif (`Playfair Display`), Sans (`Inter`), Mono (`Geist Mono` / `JetBrains Mono`) |
| **Charts** | Chart.js (`v4.4.1`) |
| **Icons** | Lucide Icons (`v0.344.0`) |
| **Audio** | Tone.js (`v14.8.49`) |

---

## Project Structure

```text
├── index.html        # Complete application (UI, probing engine, state, styles)
├── README.md         # Project documentation
└── LICENSE           # MIT License
```

---

## Quickstart

### Option 1: Direct Browser Launch
Open `index.html` directly in any modern web browser (Chrome, Firefox, Safari, Edge).

### Option 2: Local HTTP Server
To avoid local file-origin sandbox restrictions:

```bash
# Using Python 3
python -m http.server 3000

# Using Node.js (npx)
npx serve .
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## How to Integrate With Your App

### 1. Embeddable GitHub Status Badge

Add this snippet to your repository's `README.md`:

```markdown
[![Uptime Status](https://img.shields.io/badge/Uptime-99.98%25-11ff99?style=flat-square&logo=google-cloud&logoColor=white)](https://your-status-domain.com)
```

For HTML pages:

```html
<img src="[https://img.shields.io/badge/Uptime-99.98%25-11ff99?style=flat-square](https://img.shields.io/badge/Uptime-99.98%25-11ff99?style=flat-square)" alt="System Operational" />
```

---

### 2. Floating Live Web Widget

Paste this snippet just before the closing `</body>` tag of your website:

```html
<script>
(function() {
  const d = document.createElement("div");
  d.style.cssText = "position:fixed;bottom:20px;right:20px;z-index:9999;background:#0a0a0c;color:#fcfdff;border:1px solid rgba(255,255,255,0.14);padding:8px 14px;border-radius:9999px;font-family:monospace;font-size:12px;display:flex;align-items:center;gap:8px;box-shadow:0 4px 12px rgba(0,0,0,0.5);";
  d.innerHTML = '<span style="width:8px;height:8px;background:#11ff99;border-radius:50%;display:inline-block;box-shadow:0 0 8px #11ff99;"></span> Systems Operational';
  document.body.appendChild(d);
})();
</script>
```

---

### 3. Backend Heartbeat / Cron Job

For backend services, scheduled tasks, or database backups, send an HTTP GET ping upon job completion.

**cURL / Crontab**:
```bash
# Ping every 5 minutes after scheduled job completion
*/5 * * * * /usr/bin/backup-job.sh && curl -fsS --retry 3 [https://api.allorigins.win/raw?url=https://httpstat.us/200?token=YOUR_MONITOR_TOKEN](https://api.allorigins.win/raw?url=https://httpstat.us/200?token=YOUR_MONITOR_TOKEN) > /dev/null
```

**Node.js (Express / Background Worker)**:
```javascript
const https = require("https");

function pingHeartbeat() {
  https.get("[https://api.allorigins.win/raw?url=https://httpstat.us/200?token=YOUR_TOKEN](https://api.allorigins.win/raw?url=https://httpstat.us/200?token=YOUR_TOKEN)", (res) => {
    console.log(`[Pulse] Heartbeat dispatched: ${res.statusCode}`);
  }).on("error", (err) => {
    console.error(`[Pulse] Heartbeat failed: ${err.message}`);
  });
}

// Ping every 60 seconds
setInterval(pingHeartbeat, 60000);
```

**Python**:
```python
import urllib.request

def send_heartbeat():
    try:
        url = "[https://api.allorigins.win/raw?url=https://httpstat.us/200?token=YOUR_TOKEN](https://api.allorigins.win/raw?url=https://httpstat.us/200?token=YOUR_TOKEN)"
        with urllib.request.urlopen(url, timeout=5) as response:
            print(f"[Pulse] Ping successful: {response.status}")
    except Exception as e:
        print(f"[Pulse] Ping failed: {e}")

send_heartbeat()
```

---

### 4. Discord & Slack Webhooks

1. Open **Discord** (Server Settings → Integrations → Webhooks) or **Slack** (Incoming WebHooks app).
2. Copy the Webhook URL.
3. In UptimePulse, click **"Add / Edit Monitor"** or the `< >` Integrate icon on any monitor card.
4. Paste the URL into the **Alert Webhook URL** input field.
5. Click **"Test Webhook"** to send an instant test payload. When an outage occurs, an automated alert will be dispatched to your channel.

---

## Deployment

Deploying UptimePulse requires no server build step.

### GitHub Pages
1. Push this repository to GitHub.
2. Navigate to **Settings** → **Pages**.
3. Under **Build and deployment** → **Source**, select `Deploy from a branch`.
4. Choose branch `main` and folder `/ (root)`.
5. Click **Save**. Your status dashboard will be live at `https://<username>.github.io/<repo>/`.

### Vercel / Netlify / Cloudflare Pages
Drop `index.html` into a GitHub repository and link it to Vercel or Cloudflare Pages with zero build configuration (Framework Preset: `Other`, Build Command: `None`, Output Directory: `.`).

---

## Common Issues & Troubleshooting

### 1. Browser CORS Restrictions on Custom Domains
**Symptom**: Probes to certain domains show high latency or intermittent failures.  
**Fix**: Modern browsers block arbitrary cross-origin `fetch` requests. UptimePulse automatically routes web requests through an open CORS proxy (`allorigins.win`) with an image asset ping fallback. Ensure monitored endpoints allow `GET` or `HEAD` requests.

### 2. Audio Outage Alerts Not Playing
**Symptom**: Outage sound does not trigger during a simulated failure.  
**Fix**: Browsers block automatic audio playback until the user interacts with the page. Click anywhere on the dashboard once to initialize Tone.js audio playback.

### 3. LocalStorage Sandbox Restrictions in Iframes
**Symptom**: Settings or added monitors do not persist after reload inside sandboxed web previews.  
**Fix**: UptimePulse includes a built-in memory state fallback that catches and handles `SecurityError` exceptions when running inside restricted iframes. For permanent state retention, host the file on a standalone domain or GitHub Pages.

---

## Contributing

1. Fork the repository.
2. Create your feature branch (`git checkout -b feature/edge-routing`).
3. Commit your changes (`git commit -m 'Add edge routing telemetry'`).
4. Push to the branch (`git push origin feature/edge-routing`).
5. Open a Pull Request.

---

## License

Distributed under the MIT License. See `LICENSE` for more information.
