# Wallclock

A self-contained analog/digital wall clock + multi-timer + stopwatch in a single HTML file. Runs entirely in the browser — no backend, no accounts, no tracking.

## Features

### Clock
- **Analog clock** — SVG with smooth second hand animation
- **Digital time + date** — bold readable display below the clock face

### Timers
- **Multi-timer** — run multiple concurrent timers with names
- **Quick presets** — one-click 1m, 5m, 10m, 15m, 25m, 1h
- **Custom sounds** — set per-timer sound (default beep, audio file from disk, or YouTube link)
- **Drag to reorder** — fluid 2D drag-and-drop with FLIP animation
- **Persistent** — survives page reloads, runs across sessions
- **Notifications** — browser notifications + audio alarm + visual flash + title pulse when finished

### Stopwatch
- **Single stopwatch** with start/pause/lap/reset
- **Live current-lap row** — see your in-progress lap time in real time
- **Lap history** — fastest/slowest highlighted via font weight (mono palette)
- **Centisecond precision** — smooth 30fps display

### Display & Themes
- **18 themes** — 9 dark + 9 light variants
  - Dark: Midnight Rose, Forest, Ocean Deep, Sunset, Royal Velvet, Slate, Monochrome, Cherry Wine, Mint Frost
  - Light: Daylight, Ink, Paper, Citrus, Lavender, Coral, Cream, Sakura, Sage
- **Background image** — set any URL as a tinted wallpaper, with adjustable tint opacity slider
- **Wake lock** — prevents the screen from sleeping (use as a real wall clock)
- **Fullscreen mode** — distraction-free display

### General
- **Frosted-glass aesthetic** — unified blur design language across all containers
- **Persistent** — themes, timers, stopwatch state, background, all settings stored in localStorage + IndexedDB (for sound files)
- **Mobile-first** — touch-friendly, responsive, safe-area aware

## Quick Start

### Docker (recommended)

```bash
cp env.example .env    # edit PORT if needed
docker compose up -d
```

Open `http://localhost:8080`.

### Without Docker

Any static file server works:

```bash
# Python
python -m http.server 8080

# Node
npx serve -p 8080

# Or just open index.html directly
```

## Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| `PORT`   | `8080`  | Host port mapping |

Copy `env.example` to `.env` and adjust as needed.

## Deployment

The app is a single static file. Serve it from any web server, CDN, or hosting platform.

Behind **Cloudflare**: point your domain to the server, enable proxying. The file caches well at the edge. No server-side processing — all data stays in each user's browser.

## Limitations

- **YouTube on `file://`** — YouTube IFrame API (used for custom timer sounds) requires `http://` or `https://`. Use a server, not direct file:// open.
- **Wake Lock API** — not supported in older browsers. The toggle hides automatically if unsupported.
- **Notifications** — require user permission. Audio + visual alerts always work as fallback.
- **iOS Safari PWA mode** — status bar styling is fixed at parse time, may not perfectly match light themes when installed as a PWA.

## Tech Stack

- Vanilla HTML/CSS/JS — no frameworks, no build tools
- localStorage for state persistence
- IndexedDB for custom timer audio files
- Web Audio API for default beep alarm
- YouTube IFrame Player API (lazy-loaded for custom sounds)
- Notification API + Wake Lock API + Fullscreen API + Media Session API
- nginx:alpine Docker image for serving
