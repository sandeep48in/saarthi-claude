# Sarathi — Travel Guardian

> Your universal travel guardian. Plan ahead, stay safe, travel smart.

Sarathi is a free, offline-capable Progressive Web App (PWA) that acts as a personal manager, guardian, and safety officer for travellers. It plans ahead, watches the weather and the road, finds care when you need it, and keeps your essentials at thumb's reach — all without accounts, ads, or API keys.

Built for mobile from day one. Installs to your home screen. Works on any modern browser.

---

## Why Sarathi

Most travel apps fragment the journey: one for weather, one for maps, one for hotels, one for first aid. Sarathi unifies the parts that actually matter when you're on the move — planning, checklists, live conditions, nearest help, symptom triage, emergency contacts — into a single guardian that sits quietly in your pocket and speaks up only when it should.

It is built by a physician for travellers who want safety without surveillance: nothing leaves your device, no telemetry, no sign-up.

---

## Features

**Pre-Trip Planning.** Create trips with destination autocomplete, date ranges, and notes. Each new trip auto-seeds a 12-item starter checklist (documents, meds, electronics, home prep) that you can extend.

**Live Weather.** Current conditions and a 7-day forecast for both your present location and your trip destination, pulled from Open-Meteo. Proactive alerts for extreme heat, freezing temperatures, heavy rain, thunderstorms, and high UV.

**Maps & Nearby Services.** OpenStreetMap-powered map with one-tap search for nine categories — hospitals, pharmacies, clinics, police, ATMs, restaurants, fuel, hotels, toilets — sorted by distance, all via the free Overpass API.

**Health & Safety.** A rule-based symptom checker with red-flag detection for stroke (FAST signs), cardiac and respiratory emergencies, meningitis, anaphylaxis, severe abdominal events, animal bites, and heat illness. Medication tracker with dose and times. Emergency contacts with one-tap dial. Profile fields for blood group and allergies, intended for first-responder display.

**SOS Panel.** Quick-dial for 112, 911, 999, and 108 (Indian ambulance). One-tap share of your live location, one-tap "find nearest hospital", and a first-responder card that shows your name, blood group, and key medical notes.

**Smart Proactive Surfacing.** A home screen that knows the time of day, your active trip, your medication schedule, and what's coming up in the next week — and quietly tells you what matters now.

**Beautiful Mobile UI.** Bottom navigation with 44px tap targets, safe-area insets for notched phones, automatic light/dark theme, gradient hero, slide-up modals, toast notifications, smooth transitions.

**Offline-First.** Service worker caches the shell and recent API responses. Once installed, Sarathi opens and runs even without a connection — only live weather and map tiles need network.

**Data Sovereignty.** All data stays in your browser's IndexedDB. Export everything as JSON, import on another device, reset with one tap.

---

## Tech Stack

- **Vanilla HTML, CSS, JavaScript** — single-file app, no build step, no framework.
- **IndexedDB** — local persistence for trips, checklists, medications, contacts, symptom history, and settings.
- **Service Worker** — offline caching with a network-first strategy for APIs and cache-first for the shell.
- **Leaflet 1.9.4** — map rendering, loaded from CDN on demand.
- **Open-Meteo API** — weather forecasts and place geocoding (free, no key).
- **Overpass API** — OpenStreetMap point-of-interest search (free, no key).
- **Nominatim** — reverse geocoding for "you are here" naming (free, no key).
- **Browser Geolocation** — for current position (with user permission).

No backend. No accounts. No tracking. No build pipeline.

---

## File Layout

```
.
├── index.html       # The entire app — UI, logic, styles inline
├── manifest.json    # PWA manifest (name, icons, shortcuts)
├── sw.js            # Service worker (offline caching)
├── icon-192.png     # PWA icon, 192×192
├── icon-512.png     # PWA icon, 512×512
└── README.md        # This file
```

---

## Deploy with GitHub Pages

The simplest path. Free, fast, supports HTTPS (required for service workers and geolocation).

1. Push the contents of this repo to a GitHub repository.
2. Go to **Settings → Pages**.
3. Set **Source** to `main` (or `master`) branch, root folder.
4. Save. GitHub will publish your site at `https://<username>.github.io/<repo>/` within a minute.
5. Open that URL on your phone, then use the browser menu to **Add to Home Screen**.

After the first install, future updates push automatically: the next time you open the app, the service worker fetches the new `index.html` and reloads.

### Other hosting options

Any static-file host works — Netlify, Vercel, Cloudflare Pages, S3 + CloudFront, your own nginx. There is nothing to build, transpile, or compile. Just serve the files over HTTPS.

---

## Local Development

Because service workers and geolocation require a secure origin, you cannot just `file://` the HTML. Run a local server:

```bash
# Python 3
python3 -m http.server 8080

# or Node
npx serve .
```

Then open `http://localhost:8080` (treated as a secure context for development).

To force-update the service worker after edits, open DevTools → Application → Service Workers → **Update on reload**.

---

## Privacy & Data

Sarathi is built around the principle that personal travel data should never leave your device unless you choose to send it.

- All trips, checklists, medications, contacts, profile, and symptom-check history are stored in your browser's IndexedDB.
- The only network calls are anonymous, public-API requests for weather, geocoding, and POI search — they include your latitude and longitude (Open-Meteo, Overpass) but no identifying information.
- There is no analytics, no telemetry, no ad network, no third-party tracking script.
- Clearing your browser data clears Sarathi.

---

## Medical Disclaimer

The symptom checker offers general guidance using rule-based triage logic. It is **not** a diagnostic tool and is **not** a substitute for professional medical evaluation. In any emergency or when symptoms are severe, persisting, or worsening, contact local emergency services or a qualified clinician.

The author is a physician but Sarathi does not constitute a doctor-patient relationship.

---

## Roadmap Ideas

Things that may come in future versions:

- Currency converter and tipping etiquette by country.
- Public-transit overlays on the map.
- Local SIM, plug-type, and voltage information by destination.
- Vaccination and visa requirement lookups.
- Trip itinerary timeline view.
- Optional encrypted cloud sync (user-supplied storage; still no servers).
- Multi-language UI.

Suggestions and pull requests are welcome.

---

## License

MIT.

---

## Credits

- Built with care by Dr. Sandeep Bansal.
- Weather data: [Open-Meteo](https://open-meteo.com/).
- Map data: [OpenStreetMap contributors](https://www.openstreetmap.org/copyright).
- POI search: [Overpass API](https://overpass-api.de/).
- Map rendering: [Leaflet](https://leafletjs.com/).

> *Sarathi (सारथी) — a Sanskrit word meaning "charioteer" or "guide". One who steers the journey safely.*
