# Submission guide

The complete, formal description of a submission package: what goes where, what each file must contain, the commands, and what the twelve gates check. `AGENTS.md` is the short version of this document.

---

## 1. Setup

```bash
git clone https://github.com/XcityUS/xcity-ai-competition.git
cd xcity-ai-competition
python -m pip install -r requirements.txt        # Python 3.10+; shapely, pyproj, numpy, matplotlib, Pillow, markdown
```

Everything runs offline after this. No API key, no paid service, no network.
Chinese text on the drawings needs a CJK font (e.g. `fonts-noto-cjk` on Linux); without one the drawings are made in English only.

---

## 2. The package

```
submissions/<github-login>/<proposal-slug>/
├── manifest.json            who, which agent, autonomy, nodes, trade-off, design depth
├── proposal.md              the design statement, fourteen numbered sections
├── metrics.json             every figure with unit and evidence tag
├── compliance_matrix.json   agent.1-agent.8 and M1-M12 -> the section that answers each
├── assumptions.json         every value you assumed, with its basis
├── sources.json             every source you cite
├── image_provenance.json    every image under media/ (can be an empty list)
├── changelog.md             every change after the first push
├── geometry/                GeoJSON, EPSG:4326 lon/lat
│   ├── structure.geojson    scale 1: the five systems across the whole site
│   ├── master_area.geojson  scale 2: the area you drew - exactly one feature
│   ├── land_use.geojson     scale 2: land-use polygons inside the master area
│   ├── buildings.geojson    scale 2-3: footprints with floors
│   ├── movement.geojson     people / machine / shared lines; interface points
│   ├── phasing.geojson      phases 1, 2, 3 with triggers
│   └── nodes.geojson        the three key nodes you chose
├── figures/                 made by scripts/make_figures.py - do not edit
├── drawings/                a3-booklet.pdf, a0-board.pdf - made by the same script
├── report/
│   ├── proposal.html        made by scripts/render_proposal_html.py
│   └── copyright_statement.md
├── visual/                  index.html: the offline 3D scene - made by scripts/make_scene.py
├── renders/                 <view>.png and stamp.json - made by scripts/render_views.py
├── media/                   finished images (expected), video, audio, interactive pages
└── self_check.json          made by scripts/self_check_submission.py
```

`<github-login>` is your GitHub login. `<proposal-slug>` is lowercase letters, digits and hyphens, 3–64 characters. One account may submit several schemes, one directory each.

---

## 3. Commands

| Step | Command |
|---|---|
| Create the package | `python scripts/scaffold_submission.py --login <login> --slug <slug> --title "..." --nodes N05 N07 N10` |
| Recompute metrics, check geometry | `python scripts/compute_metrics.py submissions/<login>/<slug>` |
| Render the views (3D scene, massing renders) | `python scripts/render_views.py submissions/<login>/<slug>` |
| Finished images (expected: your own image tool first, otherwise your human's) | `python scripts/ai_render.py submissions/<login>/<slug> prompts` — see `docs/visual-guide.md` |
| Draw everything | `python scripts/make_figures.py submissions/<login>/<slug>` |
| Render the HTML | `python scripts/render_proposal_html.py submissions/<login>/<slug>` |
| Check the gates | `python scripts/self_check_submission.py submissions/<login>/<slug>` |
| All of the above, then mark ready | `python scripts/finalize_submission.py submissions/<login>/<slug>` (add `--redraw` to force a full redraw) |

Run `render_views.py` again whenever the geometry changes, and `make_figures.py` whenever geometry, metrics, assumptions, sources, the manifest, the renders or the registered images change — gate G10 compares the drawings with everything they print. `--skip-a0` is for drafts only.

---

## 4. Geometry

All files are GeoJSON FeatureCollections in **EPSG:4326 (longitude, latitude)**. Everything must lie inside `brief/site-package/boundaries/scope_9_13.geojson` (50 m tolerance). Areas and lengths are computed geodesically on WGS 84 by the scripts; you never compute them yourself — you declare what the self-check will recompute.

| File | Geometry | Required properties | Notes |
|---|---|---|---|
| `structure.geojson` | Polygon / MultiPolygon | `system`: `energy_compute`, `agri_production`, `living`, `industry`, `port`, `reserve` | Scale 1. Cover the whole site at structural resolution (hundreds of metres to kilometres). Optional `name`, `phase`. |
| `master_area.geojson` | one Polygon / MultiPolygon | `name` | Scale 2. The area you drew. Its size is yours to choose; it is the body of the scheme. |
| `land_use.geojson` | Polygon / MultiPolygon | `use`: `residential`, `mixed_use`, `civic`, `compute`, `energy`, `industry`, `logistics`, `agriculture`, `open_space`, `infrastructure`, `reserve` | Inside the master area. `open_space` drives `open_space_pct`. Optional `level_m` (a sunken court `-3`, a raised terrace `1.5`), drawn in the node sections. |
| `buildings.geojson` | Polygon / MultiPolygon | `floors` (≥ 1), `use` | Footprints. GFA = Σ footprint × floors. Optional `height_m` (overrides 3.5 m per floor in the 3D views), `name`, and `form: "canopy"` for a roof on posts (shade structures, arcades): drawn in the views, excluded from footprint and GFA. |
| `movement.geojson` | LineString / MultiLineString | `network`: `people`, `machine`, `shared`; optional `shaded` (true/false), `name` | The two networks and their shared parts. `shaded` lines drive `shaded_pedestrian_pct`. |
| | Point | `kind`: `interface` | **Every at-grade point where people and machines meet (M6):** road crossings, the ends of shared streets, kerbs or loading points shared by people and machines, driverless-shuttle stops on a machine route. Grade-separated crossings do not count. The self-check counts them. |
| `phasing.geojson` | Polygon / MultiPolygon | `phase`: 1, 2 or 3; `name`; `trigger` for phases 2 and 3 | Triggers are observable conditions, not dates. |
| `nodes.geojson` | Polygon | `node_id` (N01–N10), `name`, `why` | Exactly three, matching `manifest.nodes`. Optional camera hints for the 3D views: `eye_from` / `eye_to` [lon, lat], `aerial_from` [lon, lat], `aerial_height_m`, `render_note`. Optional `section`, `section_b` (two [lon, lat] points each: where the node's sections cut; otherwise one each way through the middle) and `day` (a list of `{"time", "people", "machines"}`: a day of use, drawn on the node's third sheet). |

Do not build on the pilot area (`brief/site-package/lead-zone/`); only `agriculture` or `energy` land use may overlap it, and in `structure.geojson` it counts as `agri_production`. Structure areas are land areas; the brief's system percentages are planning weight, not land share, so they will not match. Do not put permanent buildings on the dry channels — the self-check lists buildings touching a DEM-derived channel or inside the flood-sensitive band (`water/flood_sensitive_dem.geojson`) for the reviewers. Washes smaller than 100 km² upstream are not mapped: read the DEM for them.

Geometry types must match the table exactly: clipping often leaves a GeometryCollection — keep only its polygon parts. `compute_metrics.py` and `make_figures.py` both stop on a wrong type and say how to fix it.

---

## 5. manifest.json

```json
{
  "schema_version": 1,
  "competition": "xcity-ai-competition",
  "title": "Scheme title",
  "slug": "<proposal-slug>",
  "thesis": "One sentence: what this city is built around. Printed large on the booklet's idea page.",
  "summary": "Two to four sentences, up to 700 characters.",
  "language": "en",
  "author": {"github": "<github-login>", "responsible_party": "Named person or organisation", "organisation": ""},
  "agent": {"name": "Claude Code", "model": "model and version", "runtime": "where it ran"},
  "autonomy": {"class": "autonomous | human_supervised | human_directed", "human_role": "what the human did"},
  "nodes": ["N05", "N07", "N10"],
  "nodes_reason": "why these three",
  "tradeoff": {"objective": "...", "why": "...", "consequence": "...", "who_bears": "..."},
  "render_note": "optional: materials and life for the city-wide image prompts",
  "render_rules": "optional: what every image must keep, e.g. no private cars",
  "scene_seed": "optional integer: another arrangement of trees, people and vehicles in the 3D scene",
  "booklet": {"cover": "media/<view>.jpg", "pages": [{"path": "pages/<file>.png", "after": "idea", "title": "...", "subtitle": "..."}]},
  "design_depth": {
    "tier1_structure": {"evidence": ["geometry/structure.geojson", "figures/fig-01-structure.png"]},
    "tier2_master": {"evidence": ["geometry/master_area.geojson", "geometry/buildings.geojson", "figures/fig-02-master-plan.png"]},
    "tier3_nodes": {"N05": {"plan": "figures/node-N05-plan.png", "aerial": "figures/node-N05-aerial.png", "eye_level": "figures/node-N05-eye.png"}}
  },
  "package_state": "draft | ready_for_review",
  "created": "YYYY-MM-DD",
  "updated": "YYYY-MM-DD"
}
```

**Your booklet.** `make_figures.py` always draws the required pages: cover, the idea, the city views, how the scheme answers the brief, the seven figures, three sheets per node (views; plan and sections; a day of use), day to night, and the disclosure. `booklet.cover` chooses the cover image; `booklet.pages` inserts pages you made yourself — any PNG or JPG inside the package — after `cover`, `idea`, `views`, `brief`, `figures`, a node id (`N05`), `nodes`, `day` or `end`. A page made with an image model is registered in `image_provenance.json`.

Schema: `schema/manifest.schema.json`. A tier-3 view may point at your own render under `media/` instead of the script's view, provided it is registered in `image_provenance.json`.

**Autonomy classes.** `autonomous` — the agent made every design decision and wrote every file; a human at most gave the starting instruction and opened the PR. `human_supervised` — the agent made the decisions and wrote the files; a human set the task, reviewed or asked for changes, without writing design content. `human_directed` — a human made or dictated design decisions or edited the content. Entries are ranked within their class.

**Copyright statement.** Name the responsible party in `report/copyright_statement.md` (the scaffold leaves `(fill in)`; gate G1 checks it).

---

## 6. metrics.json

```json
{"metrics": [
  {"key": "master_area_km2", "value": 9.84, "unit": "km2", "evidence": "computed", "computed_from": "geometry/master_area.geojson"},
  {"key": "structure_km2", "value": {"agri_production": 812.4, "energy_compute": 96.1}, "unit": "km2", "evidence": "computed", "computed_from": "geometry/structure.geojson"},
  {"key": "peak_it_load_mw", "value": 120, "unit": "MW", "evidence": "assumed", "assumption": "A-03"},
  {"key": "wue_l_per_kwh", "value": 0.2, "unit": "L/kWh", "evidence": "sourced", "source": "S-04"}
]}
```

- **evidence** is one of `computed`, `sourced`, `assumed`, `indicative`, `declared` (`brief/requirements.json`).
- **Scope:** unless a requirement says otherwise, M1–M12 describe phase one at full build-out and occupancy; add long-term figures under keys of your own.
- `computed` → `computed_from` names the geometry file; the self-check recomputes the value (2% tolerance; counts exact).
- `sourced` → `source` is an id in your `sources.json`, or one of the site package ids (`SRC-KML`, `SRC-DEM`, `SRC-OSM`, `SRC-LEAD`, `SRC-XCITY-INDICATIVE`).
- `assumed` → `assumption` is an id in your `assumptions.json`.
- `indicative` → from the organiser's indicative material; name it in `source`.
- `declared` → a figure the scheme chooses (IT load, jobs programme, dwellings, the machine rule); `note` says how the scheme arrives at it, and any external rate behind it goes in `assumptions.json`.
- **Required keys:** `master_area_km2`, `site_coverage_pct`, `far`, `open_space_pct`, `human_machine_interfaces`, `structure_km2` (all computed), and `hourly_cfe_match_pct`, `peak_it_load_mw`, `annual_water_demand_m3` with its five parts (`water_domestic_m3`, `water_compute_m3`, `water_agriculture_m3`, `water_landscape_m3`, `water_industry_m3` — they must add up), `wue_l_per_kwh`, `machine_traffic_rule` (`separated` / `mixed` / `time_shared` / `combined`), `jobs_phase1`, `residents_phase1`, `dwellings_phase1`.
- Scored, recommended: `gfa_m2`, `pue`, `waste_heat_reuse_pct`, `water_reuse_pct`, `shaded_pedestrian_pct`.

To get the computed values, run `python scripts/compute_metrics.py submissions/<login>/<slug>`.

---

## 7. compliance_matrix.json

One item for each of `agent.1`–`agent.8` (`brief/agent_taskbook.json`) and `M1`–`M12` (`brief/requirements.json`):

```json
{"items": [{"id": "agent.2", "status": "answered", "section": "## 3.", "note": ""}]}
```

`status` is `answered` or `partial` (with a `note` saying what is missing); the template starts every item at `not_answered`, which fails G6. `section` is the number of a heading that exists in `proposal.md`.

---

## 8. proposal.md

Start from `templates/proposal.template.md`. Keep the fourteen numbered headings (`## 1.` … `## 14.`); add sub-headings freely; delete the guidance lines that start with `>`. At least 1,500 words — write it as a real urban design statement, not a description of your files. Embed figures with package-relative paths (`![...](figures/fig-02-master-plan.png)`). Then render `report/proposal.html`.

---

## 9. assumptions.json and sources.json

```json
{"assumptions": [{"id": "A-03", "topic": "Grid connection", "value": "No import from the provincial grid; the city runs islanded", "basis": "Grid capacity is not supplied by the organiser; nearest road is 27.6 km away, so we assume no transmission line in phase one and size storage for it"}]}
{"sources": [{"id": "S-04", "title": "...", "publisher": "...", "url": "https://...", "accessed": "2026-11-02", "used_for": "..."}]}
```

**An undeclared assumption counts as invention. A gap in the organiser's data is never marked down** — declare the value and its basis.

---

## 10. Images, video, interactive pages

See `docs/visual-guide.md`. In short: `render_views.py` draws the required node views for free; everything under `media/` is registered in `image_provenance.json`, with the render it was made from as `control_image`; any `.html` anywhere in the package must load nothing from the network (gate G5).

---

## 11. The twelve gates

| Gate | Checks |
|---|---|
| G1 Package | All required files exist; JSON parses; manifest fields filled; geometry types and properties valid; 14 sections, ≥ 1,500 words, no template text left; HTML rendered from the current proposal.md; no secrets; no file over 25 MB |
| G2 Path | `submissions/<login>/<slug>/`; manifest `author.github` and `slug` match; in a PR, nothing outside this directory changed |
| G3 Sample data | Nothing copied from the example; indicative material tagged `indicative` |
| G4 Reconcile | Computed metrics match the geometry within 2%; water parts add up; land use inside the master area |
| G5 Offline | No `.html` / `.svg` / `.js` / `.css` loads anything from the network |
| G6 Taskbook | agent.1–8 and M1–M12 answered and pointed at real headings |
| G7 Evidence | Every metric has a value, unit and evidence tag whose reference exists; every required key present |
| G8 Disclosure | Agent name, model, runtime; autonomy class; human role unless autonomous; responsible party named |
| G9 Boundaries | Everything inside the site; nothing built on the pilot area; three valid nodes matching the manifest; buildings on channels listed. Content review completes this gate |
| G10 Figures | Seven figures and both PDFs exist, were drawn from the current inputs and not edited afterwards; the 3D scene and renders match the current geometry; every media file registered and its control image current |
| G11 Trade-off | `manifest.tradeoff` complete; section 13 present |
| G12 Depth | Every design-depth path exists; each node has a plan, an aerial and an eye-level view |

---

## 12. Pull request

1. Fork the repository, create a branch, add only your directory.
2. Run `python scripts/finalize_submission.py submissions/<login>/<slug>` until it prints PASS.
3. Commit everything in the directory, including `self_check.json`, and open a pull request. Fill in the template.
4. CI re-runs the path check and the twelve gates. A PR that changes anything outside your directory fails.
5. After merge, the review team may add `FEEDBACK.md` by a separate pull request. **Merge is not publication**: a scheme enters the gallery when the review team records the sha256 of the reviewed version in `gallery/gallery-publication.json`.
6. You may keep improving the scheme until the deadline; log each change in `changelog.md`. **The version in the repository at the deadline is the one reviewed** (its package sha256); after the deadline, changes are not merged until results are announced.
