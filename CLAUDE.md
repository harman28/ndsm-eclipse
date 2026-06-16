# NDSM Eclipse — Project Context for Claude Code

## What this is
A single-page HTML map tool for viewing the **partial solar eclipse on 12 August 2026** from Amsterdam Noord. Built by Harman, who lives in the NDSM/Noord area.

## Files
- `index.html` — the entire app (self-contained, no build step)
- `Eclipse_Timeline.png` — official timeanddate.com eclipse phase table, shown in the sidebar

## Deployment
Static site. Push to GitHub repo `harman28/ndsm-eclipse`, enable GitHub Pages from `main` branch root. No server, no dependencies to install.

## Architecture
Pure HTML/CSS/JS. Uses:
- **Leaflet 1.9.4** (via CDN) for the map — light CARTO tile layer
- No framework, no build tool

## What the app does
- Shows a **light-themed map** centred on Amsterdam Noord / IJ waterfront
- A **red draggable dot** marks the viewpoint (default: 52°23′54.1″N 4°53′28.8″E — Noorie Point II, Johan van Hasseltkanaal mouth, near NDSM)
- Around the dot: a **compass ring** with tick marks every 15°, labelled at non-cardinal intervals, cardinal labels (N/NE/E etc.) outside the ring
- Three **eclipse phase rays** emanate from the dot to the ring:
  - **START** (blue, dashed): 19:16:05, azimuth 274°, altitude 16.1°
  - **MAX** (orange, solid): 20:10:56, azimuth 284°, altitude 8.1°
  - **END** (red, dashed): 21:03:03, azimuth 294°, altitude 0.7°
- An orange arc on the ring highlights the 274°–294° sweep zone
- Ray labels (START/MAX/END) are rendered **along** the ray, rotated to follow ray direction and always readable
- **Hover** over a ray → ray lights up (thicker, brighter), cursor becomes pointer
- **Click** a ray → Leaflet popup with event name, time, azimuth, altitude, description
- Dragging the dot redraws all rays and updates coordinate display
- **Right sidebar** shows `Eclipse_Timeline.png` (the full phase table from timeanddate.com) and the map legend
- Sidebar has a **drag handle** on its left edge — drag left to widen, right to narrow; map resizes accordingly via `map.invalidateSize()`

## Eclipse data (sourced from timeanddate.com — do not change without re-sourcing)
All times are local Amsterdam time (CEST, UTC+2), 12 Aug 2026:

| Phase   | Time     | Azimuth | Altitude |
|---------|----------|---------|----------|
| Start   | 19:16:05 | 274°    | 16.1°    |
| Max     | 20:10:56 | 284°    | 8.1°     |
| End     | 21:03:03 | 294°    | 0.7°     |

Coverage at maximum: 88%. Duration: 1h 47m. Sun sweeps W→WNW.

## Viewing location context
- Noorie Point II is at the mouth of the **Johan van Hasseltkanaal**, adjacent to **Kaap de Groene Hoop** sustainable harbour at NDSM Werf
- The IJ waterfront faces west — good unobstructed sightline toward the eclipse
- At maximum (20:11), sun is only 8.1° above horizon — any buildings/structures to the WNW matter
- The eclipse ends at 0.7° altitude; likely cut off by horizon for most ground-level viewpoints

## Known ships nearby (context for Harman)
- **Vega** (also marked "Port Vila") — tall ship / historic two-masted schooner moored at NDSM
- **Botel** — floating hotel at NDSM, visible in background with "b" and "O" neon signs

## Potential next steps / ideas discussed
- Add a **HeyWhatsThat.com**-style horizon profile overlay to show obstructions at 8° altitude
- Add **Stellarium** link for live sky simulation
- Add more intermediate phase rays (e.g. 19:32 at 277°, 19:49 at 280°) — data available in Eclipse_Timeline.png
- Mobile layout: sidebar currently stacks below map on narrow screens (CSS media query at 640px)
- Consider adding a sun altitude arc / elevation indicator alongside the azimuth compass

## Style notes
- Light theme throughout — white/cream background, no dark mode
- Font: Courier New (monospace) everywhere
- Accent colour: `#c47b00` (amber/gold) for headers and labels
- Phase colours: blue (#2196f3) for start, orange (#e67e00) for max, red (#c0392b) for end
- Keep it simple — Harman's preference is terse and functional
