# NDSM Eclipse — Project Context for Claude Code

## What this is
A single-page HTML map tool for viewing the **partial solar eclipse on 12 August 2026** from Amsterdam Noord. Built by Harman, who lives in the NDSM/Noord area.

## Files
- `index.html` — the entire app (self-contained, no build step)
- `Eclipse_Timeline.png` — official timeanddate.com eclipse phase table, shown in the sidebar
- `poster.png` — print/share poster (88% Solar Eclipse, 12 Aug 2026, NDSM Wharf, with QR code)
- `README.md` — GitHub repo landing page, displays the poster

## Deployment
Live at **https://harman28.github.io/ndsm-eclipse** — GitHub Pages from `main` branch root. No server, no dependencies to install.

## Architecture
Pure HTML/CSS/JS. Uses:
- **Leaflet 1.9.4** (via CDN) for the map — light CARTO tile layer
- **Sun position math inlined** — Meeus algorithm, equivalent to SunCalc, no extra CDN
- No framework, no build tool

## What the app does

### Map
- Light-themed map centred on Amsterdam Noord / IJ waterfront
- **Red draggable dot** marks the viewpoint (default: 52°23′54.1″N 4°53′28.8″E — Noorie Point II, Johan van Hasseltkanaal mouth, near NDSM)
- Around the dot: **compass ring** with tick marks every 15°, non-cardinal degree labels, cardinal labels (N/NE/E etc.) outside the ring
- Three **eclipse phase rays** from the dot:
  - **START** (blue, dashed): 19:16:05, azimuth 274°, altitude 16.1°
  - **MAX** (orange, solid): 20:10:56, azimuth 284°, altitude 8.1°
  - **END** (red, dashed): 21:03:03, azimuth 294°, altitude 0.7°
- Orange arc on the ring highlights the 274°–294° sweep zone
- Ray labels rendered along the ray, rotated to follow direction, always readable
- Hover over a ray → ray lights up; click → Leaflet popup with event name, time, azimuth, altitude
- **Live sun ray** (golden, #f0a500): driven by the time slider; shows current sun azimuth; fades and dashes when below horizon
- Dragging the dot redraws all rays and the sun ray; updates coordinates and Directions link

### Header (gold bar)
- Background: `#c47b00` (matches the mobile Eclipse Info tab)
- Left: title "Eclipse Viewing · 12 Aug 2026" + subtitle "Partial solar eclipse · 88% coverage"
- Right: current viewpoint coordinates + **Directions →** link (opens Google Maps, updates on drag)

### Sun slider bar
- Sits between header and map
- Range: 19:00 → ~20 min past sunset (computed dynamically via sun position math)
- Coloured tick marks at 19:16 (blue), 20:10 (orange), 21:03 (red)
- Display: time on left, azimuth + altitude stacked on right
- Moving the slider updates the golden sun ray on the map in real time

### Right sidebar
- Shows `Eclipse_Timeline.png` and the map legend (phase colours + viewpoint dot)
- Default width calculated from image aspect ratio so timeline fills the panel without overflow
- Drag handle on left edge to resize (desktop); map resizes via `map.invalidateSize()`

### Mobile layout (≤640px)
- Sidebar is hidden by default (`position: fixed`, translated down)
- Amber **▲ ECLIPSE INFO ▲** tab (48px) peeks up from the bottom; tap to toggle
- Header stacks vertically: title+subtitle / horizontal divider / coordinates + Directions side by side
- Resize handle hidden

## Eclipse data (sourced from timeanddate.com — do not change without re-sourcing)
All times are local Amsterdam time (CEST, UTC+2), 12 Aug 2026:

| Phase | Time     | Azimuth | Altitude |
|-------|----------|---------|----------|
| Start | 19:16:05 | 274°    | 16.1°    |
| Max   | 20:10:56 | 284°    | 8.1°     |
| End   | 21:03:03 | 294°    | 0.7°     |

Coverage at maximum: 88%. Duration: 1h 47m. Sun sweeps W→WNW.
`BASE_UTC = Date.UTC(2026, 7, 12, 17, 0, 0)` — 19:00 CEST = 17:00 UTC.

## Viewing location context
- Noorie Point II is at the mouth of the **Johan van Hasseltkanaal**, adjacent to **Kaap de Groene Hoop** sustainable harbour at NDSM Werf
- The IJ waterfront faces west — good unobstructed sightline toward the eclipse
- At maximum (20:11), sun is only 8.1° above horizon — buildings/structures to the WNW matter
- The eclipse ends at 0.7° altitude; likely cut off by horizon for most ground-level viewpoints

## Known ships nearby (context for Harman)
- **Vega** (also marked "Port Vila") — tall ship / historic two-masted schooner moored at NDSM
- **Botel** — floating hotel at NDSM, visible in background with "b" and "O" neon signs

## Style notes
- Font: Courier New (monospace) everywhere
- Header: gold background `#c47b00`, white text
- Body/sidebar: white/cream `#f5f5f0` background
- Accent: `#c47b00` for labels, slider, tick marks
- Phase colours: blue `#2196f3` (start), orange `#e67e00` (max), red `#c0392b` (end)
- Sun ray: `#f0a500` (golden yellow)
- No dark mode; keep it simple — Harman's preference is terse and functional

## Ideas discussed but not built
- HeyWhatsThat.com-style horizon profile overlay (obstructions at 8° altitude)
- Stellarium link for live sky simulation
- Intermediate phase rays (19:32 at 277°, 19:49 at 280°)
- Sun altitude arc / elevation indicator
- Sliding line on the Eclipse Timeline image — ruled out: table rows aren't linear time so it would feel wrong
