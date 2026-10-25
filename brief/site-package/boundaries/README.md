# Boundaries

| File | What it is |
|---|---|
| `parcels_9_13.geojson` | parcels 9 (1,483.8 km²) and 13 (172.5 km²), two features |
| `scope_9_13.geojson` | their union, 1,656.4 km², the competition site |

Both parcels' vertices come from the owner-supplied KML, unmodified: **these are exact boundaries**. Areas are geodesic on WGS 84. These files are not a cadastral record and are not for legal or contractual use.

**The overall study area of every scheme is the whole of `scope_9_13.geojson`.** All submitted geometry must lie inside this line (50 m tolerance); the self-check tests it.
