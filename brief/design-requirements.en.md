# Design requirements · XCITY AI Competition

> Machine-readable version: `brief/requirements.json`. If the two disagree, the JSON wins.

---

## A. How to read this

| Class | Meaning | If not met |
|---|---|---|
| **Mandatory M1–M12** | Must be answered | Gate G6 fails; no scoring |
| **Scored metrics** | Affect the score | Not eliminated; shows up in the relevant dimension |
| **Prohibited** | Must not appear | Review ends |

Most figures have no pass mark. The gates check **whether you gave the number, with a correct unit and a stated basis** — not whether you hit a threshold. **No number = fail. A number with its basis = pass.** How good it is belongs to scoring.

---

## B. The site: what you get and what you don't

### B.1 Extent

| | Area | Source | Confidence |
|---|---|---|---|
| Parcel 9 | 1,483.8 km² | Owner KML | Exact |
| Parcel 13 | 172.5 km² | Owner KML | Exact |
| Together (the site) | 1,656.4 km² (quoted as 1,656 km²) | Union | Exact |
| Pilot area (not open to design) | 13.9 km² | XCITY | — |

All submitted geometry lies inside `brief/site-package/boundaries/scope_9_13.geojson` (50 m tolerance) and nothing may be built on the pilot area.

### B.2 Supplied

See `brief/site-package/README.md`. Cite the matching `SRC-*` id in your `sources.json`. Indicative zoning (`zoning/indicative_systems_9_13.json`) is cited as `indicative` only — never measured or approved.

### B.3 Not supplied

| Data | Held by |
|---|---|
| Official cadastre | Dirección de Geodesia y Catastro, San Juan |
| Grid connection and capacity | Provincial utility |
| Water rights and abstraction | Provincial water authority |
| Seismic code edition | INPRES / CIRSOC |
| Climate series | See `site-package/climate/README.md` |

**You may assume — in `assumptions.json`, with the value, its source and the reason. An undeclared assumption counts as invention.** **A gap in the data the organiser supplied is never a reason to mark an entry down.**

---

## C. Hard conditions of the site

These are design constraints, not background. A scheme that shows no trace of them scores low on D1.

1. **Earthquakes.** State the structural system and seismic strategy and what they do to heights, spacing and refuge space.
2. **The Zonda.** State the stance — block, channel or step aside — and carry it into street orientation, sections and equipment intakes.
3. **Dry channels and flash floods.** **No permanent construction on a dry channel.** Mark the flood corridors in your geometry and state the basis for their width. Terrain-derived channels are in `site-package/water/channels_dem.geojson`; the self-check lists any building that touches one for the reviewers.
4. **Dark sky.** Give a night-lighting and light-pollution strategy.
5. **No road.** The access corridor is part of phase-one works; draw it.
6. **The pilot area and its under-panel system.** Unchanged; the city grows beside it.

---

## D. Mandatory M1–M12

Each one gets a status in `compliance_matrix.json` pointing at the section of `proposal.md` that answers it. Where a metric key is given, declare the value, unit and evidence tag (computed / sourced / assumed / indicative / declared) in `metrics.json` as well. **Unless stated otherwise, M1–M12 describe phase one at full build-out and occupancy.**

**M1 · Hourly carbon-free energy match** (`hourly_cfe_match_pct`, %) — share of hours in a representative year whose use is covered by carbon-free power in the same hour. State the generation mix, storage duration, and whether the match is **physical** or **contractual**. Daytime solar is easy; this is about the night.

**M2 · Peak IT load in phase one** (`peak_it_load_mw`, MW) — with the grid capacity you assumed. For scale: 40 MW is roughly a 20,000–30,000 m² data hall.

**M3 · Annual water demand** (`annual_water_demand_m3`, m³/yr) — by use: `water_domestic_m3`, `water_compute_m3`, `water_agriculture_m3`, `water_landscape_m3`, `water_industry_m3`. **The five must add up to the total (2% tolerance)**; the self-check tests it. Say which line panel-cleaning water sits in.

**M4 · Cooling WUE** (`wue_l_per_kwh`, L/kWh) — with the cooling type (air / liquid / hybrid / dry) and the PUE that goes with it. Air saves water and costs power; liquid the reverse. Claiming both is not accepted.

**M5 · A 30% water shortfall** — 30% less water than your phase-one demand (M3). Which use stops first: a priority order, what happens in the city at each step, how many people are affected, and whether compute load comes down with it.

**M6 · Human-machine at-grade interfaces** (`human_machine_interfaces`, count) — where autonomous machines and pedestrians meet on the same level: road crossings, the ends of shared streets, kerbs or loading points shared by people and machines, driverless-shuttle stops on a machine route; grade-separated crossings do not count. **Mark each one in `geometry/movement.geojson` as a Point with `kind: "interface"`**; the self-check counts them and the declared value must match.

**M7 · Machine traffic rule** (`machine_traffic_rule`: `separated` / `mixed` / `time_shared` / `combined`) — where each rule applies and how it is enforced.

**M8 · Public audit mechanism** — who publishes power, water, generation and compute-load data, how often, and who can check it independently.

**M9 · Control and succession of the compute asset** — who owns and runs it, and what happens if that operator leaves.

**M10 · Triggers for phases two and three** — population, occupancy, grid capacity, water: **observable** conditions, not a timetable.

**M11 · Irreversible decisions** — at least three phase-one decisions that cannot be changed later, and why that is acceptable.

**M12 · Jobs, residents and dwellings reconcile** (`jobs_phase1`, `residents_phase1`, `dwellings_phase1`) — if residents far outnumber jobs, who the others are and what they live on.

---

## E. Scored metrics

| Metric | Key | Unit | Note |
|---|---|---|---|
| Waste-heat reuse | `waste_heat_reuse_pct` | % | Name the receiver |
| PUE | `pue` | ratio | Consistent with the cooling type in M4 |
| Water reuse | `water_reuse_pct` | % | Treatment level and reuse |
| Shaded share of the main pedestrian network | `shaded_pedestrian_pct` | % | Whether walking works at all in a desert |

### Recomputed from geometry (gate G4, 2% tolerance)

Declared with evidence tag `computed`; the self-check recomputes them:

| Metric | Key | How |
|---|---|---|
| Master design area | `master_area_km2` | Geodesic area of `master_area.geojson` |
| Site coverage | `site_coverage_pct` | Building footprint ÷ master area |
| Gross floor area | `gfa_m2` | Σ footprint × floors |
| Floor area ratio | `far` | GFA ÷ master area |
| Open space share | `open_space_pct` | `open_space` in `land_use` ÷ master area |
| Human-machine interfaces | `human_machine_interfaces` | Points with `kind: interface` in `movement.geojson` |
| Area per system | `structure_km2` | `structure.geojson` summed by `system` |

`master_area_km2`, `site_coverage_pct`, `far`, `open_space_pct`, `human_machine_interfaces` and `structure_km2` are required. **Do not enter a good-looking number; enter one that can be computed.**

---

## F. Prohibited

Any one ends the review:

1. Personal data, confidential material or non-public spatial data
2. A claimed official endorsement, approval or statutory conclusion
3. Discriminatory or harmful content
4. Off-topic material
5. Changes to any file outside your own submission directory

These **do not count as answers**: an adjective without a number; a reduction claim with no baseline; waste-heat reuse with no named receiver; a water-shortage response with no priority order; a jobs figure with no skills mix and no named trainer.

---

## G. Deliverables

Format and commands: `docs/submission-guide.md`. Drawings and renders: `docs/visual-guide.md`.
