# UptimePulse

> A lightweight, self-contained uptime monitoring dashboard and public status page with an editorial developer interface.

_Assumes a single-file deployment (`index.html`) hosted directly via GitHub Pages, Vercel, or any static HTTP server._

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
└── LICENSE           # MIT License# UptimePulse

> A lightweight, self-contained uptime monitoring dashboard and public status page with an editorial developer interface.

_Assumes a single-file deployment (`index.html`) hosted directly via GitHub Pages, Vercel, or any static HTTP server._

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
