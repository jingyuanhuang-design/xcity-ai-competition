# Site package

**XCITY AI Competition · Parcels 9 and 13 · 1,656 km² · San Juan, Argentina**

Everything the organiser supplies about the site is in this folder. Coordinates are EPSG:4326 (WGS 84 lon/lat) unless a file says otherwise. Sources and licences: `sources.json`. File list and checksums: `datapackage.json`. Every area figure: `areas.json`.

| File | What it is | Confidence |
|---|---|---|
| `boundaries/parcels_9_13.geojson` | the two parcels | exact, owner KML |
| `boundaries/scope_9_13.geojson` | their union = the site | exact |
| `lead-zone/lead_zone.geojson` | pilot area, built first, **not open to design** | organiser |
| `access/roads_osm.geojson` | nearest national and provincial roads | OpenStreetMap |
| `access/road_distances_9_13.json` | shortest distance from the site to each road | computed |
| `water/channels_dem.geojson` | seasonal channels derived from the DEM (upstream area ≥ 100 km²) | derived, not surveyed |
| `water/flood_sensitive_dem.geojson` | flood-sensitive band, 503 km² (defined in terrain_summary) | derived |
| `terrain/dem_9_13_utm19s_60m.tif` | elevation (GeoTIFF) | Copernicus DEM GLO-30 |
| `terrain/dem_9_13_utm19s_60m.png` | the same DEM as a 16-bit PNG, value = metres | same |
| `terrain/hillshade_9_13.png` / `hillshade_9_13_utm.png` | hillshade basemaps (lon/lat and UTM) | derived |
| `terrain/terrain_summary_9_13.json` | slope classes, flood band, elevation | computed |
| `zoning/indicative_systems_9_13.json` | indicative positions of the five systems | **indicative only** |
| `nodes/design_nodes.json` | ten key nodes, choose three | — |
| `climate/README.md` | climate: where to get it and how to declare it | — |

## Site facts

| | |
|---|---|
| Site | 1,656 km² (parcel 9: 1,483.8 · parcel 13: 172.5) |
| Pilot area | three fields, 13.9 km², inside parcel 13 |
| Slope < 2% | 1,183 km² |
| Slope ≥ 25% (mountain) | 127 km², mostly the Pie de Palo range in the south-east of parcel 9 |
| Flood-sensitive | 503 km² |
| Flat and clear of flood | 686 km² |
| Elevation | 606–2,658 m, median 675 m |
| Roads on site | **none**; nearest, RN 40, about 27.6 km |

## How to cite

- Cite the matching `SRC-*` id in your own `sources.json` for any figure taken from here.
- Anything from `zoning/indicative_systems_9_13.json` carries the evidence tag `indicative` — never measured or approved.
- Channels are terrain-derived flow lines drawn down to 100 km² upstream area; read smaller washes from the DEM yourself. Flood peaks are not supplied: write the value you used into `assumptions.json`.
- **A gap in the data the organiser supplied is never a reason to mark an entry down.** Declare the value you used and where it came from, and the requirement is met.

## Not supplied

| Data | Held by | What to do |
|---|---|---|
| Official cadastre | Dirección de Geodesia y Catastro, San Juan | use the KML boundaries here |
| Grid connection and capacity | provincial utility | assume and declare |
| Water rights and abstraction | provincial water authority | assume and declare |
| Seismic code edition | INPRES-CIRSOC 103 | declare the edition you used |
| Climate series | see climate/README.md | obtain and declare |

## Licences

- Terrain-derived data: produced using Copernicus WorldDEM-30 © DLR e.V. 2010-2014 and © Airbus Defence and Space GmbH 2014-2018 provided under COPERNICUS by the European Union and ESA; all rights reserved. The organisations in charge of the Copernicus programme by law or by delegation do not incur any liability for any use of the Copernicus WorldDEM-30.
- Roads: © OpenStreetMap contributors, ODbL 1.0.
- Parcel boundaries, pilot area and indicative zoning are provided by XCITY for this competition only; not a cadastral record and not for legal use.
