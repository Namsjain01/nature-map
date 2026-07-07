# Map of Nature Experiences

A living, interactive globe of nature experiences across the world, made for **Order of the Wild** ([wild.community](https://wild.community)).

**🌍 Live site:** https://namsjain01.github.io/nature-map/

## What it is

Open the site and you arrive at a poetic intro screen. One click takes you to a realistic 3D Earth floating in space, dotted with glowing map pins. Each pin is a real place — a forest school, a wilderness guide, a rewilding project, or a transformative travel experience — currently 71 of them across roughly 24 countries, gathered from publicly available sources. Thin arcs of light weave related places together so the network reads as a living constellation rather than a list.

The map exists to help people find local, meaningful experiences in and with nature, and to make the growing network of nature schools and guides visible as one connected whole.

## What you can do on it

- Spin and zoom the globe freely; hover a pin for a quick preview, click it for the full story (description, location, website link, "suggest an edit").
- Search by name, place or practice, filter by category, or press **"Find experiences near me"** to sort by distance from you.
- Take four **guided journeys** that fly across themed collections (e.g. forest schools of Europe).
- Switch to a **street map mode** for finding places up close.
- Keep zooming out and you leave the atmosphere entirely — the Moon, Sun, and planets on their orbit rings, with a handwritten note pointing at Earth.

## How it's built

Everything is **one self-contained file** — [`index.html`](index.html). No build step, no bundler, no server code, no API keys. Open it in a browser and it runs. All dependencies load from CDNs, so it needs an internet connection to render.

- **[globe.gl](https://github.com/vasturiano/globe.gl) v2** — the 3D globe (WebGL via three.js).
- **three.js 0.161** — imported dynamically inside the script for custom objects (pins, Sun, planets, Moon, annotations).
- **MapLibre GL v5** + **CARTO basemaps** — the optional street map mode (free, no token).
- **Fonts:** Fraunces (display) + Inter (UI) from Google Fonts.

## Hosting & deployment

This repo is served by **GitHub Pages** from the `main` branch root, so `index.html` is the live page. Deployment is simply **commit + push** — Pages rebuilds in ~1–2 minutes.

```bash
# after editing index.html
git add index.html
git commit -m "Update map"
git push origin main
```

## Updating the data

All entries live in one clearly-marked array near the top of the `<script>` section (search for `DATA`). Each entry:

```js
{
  "id": 123,                  // any unique number
  "name": "Forest School X",
  "url": "https://...",       // optional; hides the website button if empty
  "desc": "Description text",
  "loc": "City, Country",
  "lat": 51.5, "lng": 6.8,
  "cat": "school",            // school | experience | guide | rewilding
  "oow": false,               // true = gold "OOW Tested and Loved" star
  "country": "Germany",       // used by search and the intro country count
  "img": "https://.../a.jpg"  // optional photo, shows in tooltip and detail panel
}
```

Keep valid JSON per entry (double quotes, commas between entries) — a single syntax error stops the whole script.

## Embedding on a website

Drop an iframe pointing at the hosted URL:

```html
<iframe
  src="https://namsjain01.github.io/nature-map/?embed=1&theme=light"
  width="100%" height="700"
  style="border:0; border-radius:12px;"
  allow="geolocation"
  loading="lazy"
  title="Map of Nature Experiences">
</iframe>
```

**URL parameters:**

- `?embed=1` — skips the poetic intro (recommended inside an embed).
- `?theme=light` / `?theme=dark` — forces a theme; omit to follow the visitor's system preference.
- `?view=map` — starts in street map mode.
- `allow="geolocation"` on the iframe is required for the "Find experiences near me" button.

## Status

This is a **prototype**. It collects no data, has no accounts and no tracking. The feedback and submission buttons link to Order of the Wild's own public forms.
