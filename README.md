# ARES – Mars Surface Operations Dashboard (static site)

Entry point: `index.html` (single file, ~17.5 MB). Both scientific datasets are embedded in it.
No build step, no server code, no browser storage.

## Deploy on Netlify (not yet done)
Option A – drag and drop: sign in at app.netlify.com → Sites → "Add new site" → "Deploy manually" →
drop this whole `ares-site` folder. Netlify gives you an https://<name>.netlify.app URL.

Option B – CLI: `npm i -g netlify-cli`, then in this folder run `netlify deploy --prod --dir .`
(first run asks you to log in and create/link a site).

After deploying, work through the checklist in `../TEST-REPORT.md` → "Still to do on the live URL".

## External services
| Purpose | Service | Used by |
|---|---|---|
| Leaflet 1.9.4 JS+CSS | unpkg.com (fallback: cdn.jsdelivr.net) | map |
| Fonts: Inter, JetBrains Mono, Orbitron | fonts.googleapis.com / fonts.gstatic.com | all text (system fallbacks in CSS) |
| MOLA Elevation base layer, Viking MDIM 2.1 | s3-eu-west-1.amazonaws.com/whereonmars.cartodb.net | map tiles |
| THEMIS Day / Night IR | planetarymaps.usgs.gov (WMS) | map tiles |

Tailwind: no CDN. The Tailwind CSS generated in the original page is kept verbatim in a `<style>` block,
plus `#tailwind-supplement` (3 utilities used only in Critical states).

## Real data vs demonstration values
* MOLA elevation (embedded `megt00n090hb`): real NASA data, **only 0°–44°S, 90°E–180°E**, ~0.9 km pixels, 4 m steps.
* THEMIS temperature (embedded `I01443004PBT`): real NASA data, **only a ~3° wide strip, 12.9°S–5.2°N around 139.5°E**.
* Outside the MOLA tile, map-click waypoints get a **random DEMO elevation** (existing app behaviour, tagged "DEMO").
  The default map view (18.38°N, 77.58°E) is outside the tile, so a first click there is a DEMO value.
* Suit O₂/battery, walking speeds and slope thresholds are the app's own model, not measurements.
* The map base imagery is not embedded; it comes from the services above.

## Limitations
See `../TEST-REPORT.md`.
