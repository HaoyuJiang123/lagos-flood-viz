# Lagos Flood Exposure — Web Map

Interactive Leaflet map showing Event-based Flood Exposure Index (EFEI) for Lagos
across three extreme rainfall events (2018, 2021, 2024).

## File Structure

```
project/
├── index.html              ← open this in a browser
└── overlays/
    ├── event_A.png         ← EFEI classes, Event A (2021-08-29 → 09-04)
    ├── event_B.png         ← EFEI classes, Event B (2018-09-05 → 09-11)
    ├── event_C.png         ← EFEI classes, Event C (2024-10-12 → 10-18)
    ├── diff_BA.png         ← Difference map (Event B − Event A)
    ├── hotspots.png        ← Persistent high-risk hotspots
    └── metadata.json       ← Bounds + stats (reference)
```

## How to View

### Locally
**The HTML won't load the PNG overlays from `file://` in most browsers.**
Run a local server from the project folder:

```bash
# Python (most systems)
python3 -m http.server 8000

# then open:
# http://localhost:8000
```

Or use VS Code with the Live Server extension — right-click `index.html` → "Open with Live Server".

### On GitHub Pages
1. Put the whole `project/` folder contents at the root (or a sub-folder) of a GitHub repo.
2. Enable GitHub Pages in repo Settings → Pages.
3. Visit `https://<username>.github.io/<repo-name>/`.

## Features

- **Event switcher** (top-right) — tab between A / B / C
- **Event details** — dates, mean 7-day rainfall, real-world historical context
- **Stats panel** (bottom-right) — live % and km² for Low / Medium / High exposure
- **Legend + layer controls** (bottom-left):
  - Toggle the event exposure layer
  - Toggle the persistent-hotspot layer (pixels that are HIGH-risk in all three events)
  - Toggle the B − A difference map
  - Opacity slider
- **Methodology button** (bottom-centre) — opens a modal with the rainfall-threshold
  definition, EFEI formula, data sources, and class reading.

## Data Layers Explained

| Layer            | Meaning                                                               |
| ---------------- | --------------------------------------------------------------------- |
| Event A/B/C      | EFEI class per pixel (1 = Low, 2 = Medium, 3 = High)                  |
| Difference B − A | Red = exposure **increased** in B vs A; Blue = exposure **decreased** |
| Hotspots         | How many of the 3 events a pixel is High-risk (colour = 1, 2, or 3)   |

**EFEI formula:**
`EFEI = 0.3 × Elevation_risk + 0.3 × Water_proximity_risk + 0.4 × Rainfall_risk`

All three components normalised to 0–1 before combination.

## Data Sources

- Rainfall: CHIRPS Daily (UCSB-CHG), 2015 – 2024
- Elevation: NASA NASADEM_HGT (~30 m)
- Surface water: JRC Global Surface Water v1.4
- Processing: Google Earth Engine → GeoTIFF → indexed PNG overlays

## Bounds

The overlays cover 3.000°E – 4.200°E and 6.300°N – 6.851°N
(i.e. Lagos metropolitan area and surroundings).
