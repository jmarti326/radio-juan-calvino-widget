# Radio Juan Calvino — Widget

A beautiful, self-contained web radio player for **Radio Juan Calvino**
(*Iglesia Presbiteriana Reformada del Caribe – OPC*), built as a friendlier,
more modern replacement for the default RadioJar embed.

It plays the church's live RadioJar stream and shows real-time **"now playing"**
track info (title, artist, album, artwork) pulled from RadioJar's public API.

![style: glassmorphism](https://img.shields.io/badge/style-glassmorphism-a72020)
![deps: none](https://img.shields.io/badge/dependencies-none-3d90be)

---

## ✨ Features

- **Live stream playback** via HTML5 audio (`https://stream.radiojar.com/usdyrun8zccwv`).
- **Now Playing** — title, artist, album and cover art, auto-refreshed every 15s.
- **Brand-matched design** — church colors (maroon `#832521`, red `#a72020`,
  blue `#3d90be`) and fonts (Poppins + Montserrat).
- **Glassmorphism UI** — animated glow, "EN VIVO" pulse, breathing album art,
  animated equalizer while playing.
- **Accessible** — keyboard controls (Space = play/pause), ARIA labels,
  focus outlines, and `prefers-reduced-motion` support.
- **Zero dependencies, no build step** — a single `index.html` you can host anywhere.
- **HTTPS-safe** — avoids mixed-content blocking; RadioJar nodes serve audio
  over HTTPS, so it works embedded on the HTTPS church site.

---

## 🚀 Quick start (embed)

Publish `index.html` (see [Deployment](#-deployment)) and drop this into any page:

```html
<iframe
  src="https://jmarti326.github.io/radio-juan-calvino-widget/"
  title="Radio Juan Calvino"
  style="border:0;width:100%;max-width:410px;height:250px;"
  scrolling="no" loading="lazy" allow="autoplay">
</iframe>
```

On the current church site the default player lives inside the
`.church-info-bar` block — replace that RadioJar `<iframe>` with the one above.
See [`embed-example.html`](./embed-example.html) for copy-paste snippets.

> **Recommended iframe size:** ~`380–410px` wide × `250px` tall.

---

## 🖥️ Local preview

No build tools required — just serve the folder:

```powershell
# Python
python -m http.server 8080
# then open http://localhost:8080

# …or Node
npx serve .
```

Open `index.html` directly (`file://`) also works, though a local server better
matches production behavior.

---

## 🌐 Deployment

### Option A — GitHub Pages (included workflow)
This repo ships with `.github/workflows/deploy-pages.yml`, which publishes the
site automatically on every push to `main`.

1. Push this repo to GitHub.
2. **Settings → Pages → Build and deployment → Source: GitHub Actions.**
3. Your widget will be live at
   `https://jmarti326.github.io/radio-juan-calvino-widget/`.

> **Private repos:** GitHub Pages from a **private** repository requires a paid
> plan (GitHub Pro/Team/Enterprise). If you're on Free, either make the repo
> public or use Option B.

### Option B — any static host
Because it's a single static file, you can drop `index.html` on **Netlify,
Vercel, Cloudflare Pages, or the church's own web server** with no
configuration.

---

## ⚙️ Configuration

All settings live in one `CONFIG` block near the top of the `<script>` in
[`index.html`](./index.html):

| Key           | Purpose                                             |
|---------------|-----------------------------------------------------|
| `stationId`   | RadioJar station id (from the stream URL).          |
| `streamUrl`   | Audio stream (keep `https://` for mixed-content safety). |
| `metaUrl`     | Now-playing JSON endpoint (CORS-enabled).           |
| `pollMs`      | How often to refresh track info (ms).               |
| `fallbackArt` | Cover shown when a track has no artwork.            |
| `stationName` | Display name in the header.                         |

### Stream URLs (reference)
- **MP3:** `http://stream.radiojar.com/usdyrun8zccwv`
- **M3U:** `http://stream.radiojar.com/usdyrun8zccwv.m3u`
- **PLS:** `http://stream.radiojar.com/usdyrun8zccwv.pls`

The widget uses the `https://` form of the MP3 stream so it plays without
mixed-content warnings when embedded on an HTTPS page.

---

## 📁 Structure

```
radio-juan-calvino-widget/
├─ index.html                 # the whole widget (HTML + CSS + JS)
├─ embed-example.html         # copy-paste iframe snippets
├─ .gitignore
├─ .github/workflows/
│  └─ deploy-pages.yml        # GitHub Pages deploy
└─ README.md
```

---

## 📝 Notes

- The "now playing" endpoint returns `access-control-allow-origin: *`, so the
  browser fetch works cross-origin from any site.
- If RadioJar's metadata is temporarily unavailable, the player still streams —
  metadata is best-effort and fails silently.

---

*Built for the Iglesia Presbiteriana Reformada del Caribe (OPC).*
