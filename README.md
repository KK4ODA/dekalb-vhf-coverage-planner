# DeKalb County VHF Coverage Planner

Terrain-aware VHF radio coverage planning tool for DeKalb County Fire Rescue (DCFR) EMCOMM/ARES operations.

## Overview

A single-file HTML application that models VHF propagation across DeKalb County, Georgia using the Okumura-Hata suburban model with effective antenna height correction and Bullington single knife-edge diffraction. An embedded 13,431-point Digital Elevation Model (DEM) derived from USGS NED control points provides terrain data without any runtime API calls.

## Features

**35 Deployment Sites** across 4 categories:
- 26 DCFR fire stations
- 3 Mountain summits (Stone Mountain, Arabia Mountain, Pine Mountain)
- 3 Command/infrastructure sites (EOC, DCFR HQ, Doraville PD)
- 3 Hospitals (Emory Decatur, Emory Hillandale, Children's Healthcare)

**4 Analysis Modes:**
1. **Field Coverage** — per-station coverage polygon with adjustable power, antenna height, and receiver sensitivity; optional -25% derate for conservative planning
2. **Station-to-Station Links** — all-pairs link budget between selected stations with PASS/MARGINAL/FAIL classification
3. **Frequency Planning** — 3-tier frequency architecture (county tactical, SR zone, local tac) with CTCSS tone assignments deconflicted against metro Atlanta repeaters; simplex repeater (SR) designation
4. **Path Diagnostic** — point-to-point link budget with SVG terrain profile, Fresnel zone visualization, and field/base radio toggle

**Propagation Models:**
- Okumura-Hata suburban path loss (150-1500 MHz)
- Effective antenna height: h_b(eff) = mast + max(0, Δelevation), clamped to [mast, 300m]
- Bullington single knife-edge diffraction loss
- Fresnel zone clearance analysis

**Frequency Plan:**
- Tactical net: 146.460 MHz (county-wide, no CTCSS)
- North SR zone: 147.420 MHz / 141.3 Hz CTCSS
- South SR zone: 147.510 MHz / 186.2 Hz CTCSS
- Local tac: 446.000 MHz UHF (no CTCSS)

## Usage

Open `dekalb_vhf_planner.html` in any modern web browser. No server, build step, or internet connection required (map tiles excepted).

1. Select stations from the left panel
2. Choose an analysis mode from the tabs
3. Adjust propagation parameters (power, antenna height, sensitivity) as needed
4. Click stations on the map to set TX/RX endpoints in Path Diagnostic mode

## Files

| File | Description |
|------|-------------|
| `dekalb_vhf_planner.html` | Main application (single-file, ~155 KB) |
| `DeKalb_VHF_Coverage_Planner_Manual.docx` | User and reference manual (v1.3) |

## Technical Notes

- **DEM Grid:** 111×121 points, 0.01° step, covering 33.25-34.35°N / 84.75-83.55°W
- **Coverage polygons:** 36-radial sweep with 2-pass neighbor smoothing (1.4× clamp)
- **Map:** Leaflet.js with CartoDB Dark Matter tiles
- **County boundary:** OSM Nominatim GeoJSON (fetched at load)

## License

MIT

## Author

Facundo — KK4ODA
