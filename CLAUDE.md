# NDSM Eclipse — Project Context for Claude Code

Single-page HTML map for viewing the partial solar eclipse on **12 August 2026** from Amsterdam Noord. Built for Harman at NDSM/Noord.

**Live:** https://harman28.github.io/ndsm-eclipse (GitHub Pages, `harman28/ndsm-eclipse`, main branch)

## Files
- `index.html` — entire app, self-contained, no build step
- `Eclipse_Timeline.png` — timeanddate.com phase table, shown in sidebar
- `poster.png` — print/share poster with QR code

## Stack
Leaflet 1.9.4 (CDN), sun position math inlined (Meeus algorithm), no framework.

## Eclipse data — do not change without re-sourcing from timeanddate.com
All times CEST (UTC+2), 12 Aug 2026. `BASE_UTC = Date.UTC(2026, 7, 12, 17, 0, 0)`

| Phase | Time     | Azimuth | Altitude |
|-------|----------|---------|----------|
| Start | 19:16:05 | 274°    | 16.1°    |
| Max   | 20:10:56 | 284°    | 8.1°     |
| End   | 21:03:03 | 294°    | 0.7°     |

Coverage 88%. Default viewpoint: 52°23′54.1″N 4°53′28.8″E (Noorie Point II, NDSM).

## Style
- Gold header `#c47b00` (bg), white text. Body: white/cream.
- Font: Courier New everywhere. No dark mode.
- Phase colours: blue `#2196f3` / orange `#e67e00` / red `#c0392b`. Sun ray: `#f0a500`.

## Ideas not yet built
- Horizon profile overlay (HeyWhatsThat-style, obstructions at 8°)
- Stellarium link
- Intermediate phase rays (19:32 at 277°, 19:49 at 280°)
