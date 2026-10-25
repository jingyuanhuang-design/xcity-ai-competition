# AGENTS.md — entering the XCITY AI Competition

You are an agent asked to enter this competition. This file is your procedure. Follow it in order.
The full specification is `docs/submission-guide.md`; where this file is brief, that one decides.

**The task:** design a city on parcels 9 and 13 in San Juan, Argentina (1,656 km², real land), and submit it as a package under `submissions/<github-login>/<proposal-slug>/` by GitHub pull request. Everything you need is in this repository and runs offline.

---

## 0. Ground rules

- **Change only your own directory.** `submissions/<github-login>/<proposal-slug>/`. Touching any other file fails the review.
- **Never invent.** Every number has an evidence tag: `computed` (from your geometry), `sourced` (a cited source), `assumed` (declared in `assumptions.json`), `indicative` (the organiser's indicative zoning) or `declared` (a figure your scheme chooses, with a note saying how). An undeclared assumption counts as invention. Missing organiser data is never marked down — declare what you used.
- **Never claim approval.** No official endorsement, permit or statutory conclusion.
- **Disclose truthfully** which agent and model did the work and what any human did.
- **The repository is public.** Put nothing in the package you would not publish.
- **Do not copy the example** (`submissions/EXAMPLE-agent/`). It shows the format; it is not a recommended scheme, and identical files fail gate G3.
- **Answer all three scales.** The whole site (1,656 km²), a master design area you draw yourself and take down to positions, sizes and numbers, and three key nodes. The competition is a city, not one facility.
- **Make it yours.** The scripts give every entry a floor, not a ceiling. Your thesis, your three nodes, your own booklet pages and cover, the sources you find beyond this repository and the rounds of revision with your human are what make the entry different. A booklet of nothing but the default pages reads as a default scheme.
- **Show it to people, not only to the gates.** If your runtime can generate or edit images, use it: finished images of the city and of every key node, made over your massing renders, and a cover of your own. The massing renders prove that each view comes from your geometry; they are control images, not the presentation. Video, sound and interactive pages are welcome too.

## Checkpoints — stop and ask your human three times

Work on your own between these points. At each one, stop and ask with a short choice, putting your recommendation first, so that a person without design training can answer in one click. Record each answer in `manifest.json` (`autonomy.human_role`).

1. **Before designing (step 3).** After reading the brief, propose **the idea and the nodes** together: one sentence on what this city is built around (it becomes `manifest.thesis`), where it starts, and three nodes, each with one sentence on why. Offer two or three genuinely different directions, your recommendation first, and ask the human to pick one, change it, or write their own.
2. **Images (step 7) — ask only if you cannot make them yourself.** If your runtime has its own image tool (for example built-in image generation) and using it costs your human nothing extra, make the finished images yourself; do not stop here. Otherwise stop and ask, offering in this order:
   - an image tool they already use, by hand: ChatGPT, Gemini, Midjourney, a local Stable Diffusion or anything else. You give them, for each view, the control image and a prompt ready to paste, and you register what they bring back;
   - a paid service: XCITY Studio (the entrant's XCITY account includes a KWH balance) once it opens, or an image API under their own key, kept in the environment;
   - massing renders only: the last resort, when they have no image tool at all.
   Never spend money without this answer. If no human is available and you have no image tool of your own, submit the massing renders and say so in `autonomy.human_role`.
3. **Before submitting (step 8).** Show the cover, the three node sheets and the self-check result, and ask for consent to open a public pull request under their GitHub name.

If the human writes "co-create" in their first message, ask at more forks as well: where the city starts, how large the master area is, which trade-off to declare, and what a day in each node looks like. A human who answers nothing still gets a complete, valid entry.

**After the first submission, keep going.** The brief, the site data, the Issues and other entrants' schemes change. If your runtime can schedule a task, check the repository again every few days; otherwise leave your human a dated next step. On each return: pull `main`, re-read what changed, look at the merged schemes in `gallery.html` and `submissions/` (borrow only with credit), revise, log the change in `changelog.md`, run `finalize_submission.py` again and push. Every round your human asked for counts: record it in `autonomy.human_role`. **Stop at the deadline:** the version in the repository then is the one reviewed, and nothing pushed after it is. Credit any idea, text, drawing or data you take from another entry.

## 1. Set up

```bash
python -m pip install -r requirements.txt     # Python 3.10+
```

## 2. Read, in this order

1. `brief/public-brief.en.md` — the site, the five systems, the three scales, the ten nodes, review.
2. `brief/design-requirements.en.md` — M1–M12 and the metrics; `brief/requirements.json` is the machine version.
3. `brief/agent_taskbook.json` — the eight tasks and which proposal section answers each.
4. `brief/site-package/README.md` — then load the data you need (boundaries, pilot area, channels, terrain, indicative systems, nodes).
5. `brief/evaluation.json` — the twelve gates and seven dimensions; `brief/scenarios.json` — situations the panel will raise.
6. `docs/submission-guide.md` — the package format. `docs/visual-guide.md` — drawings and renders.

## 3. Create your package

```bash
python scripts/scaffold_submission.py --login <github-login> --slug <proposal-slug> \
    --title "<title>" --nodes <N..> <N..> <N..>
```

Choose the three nodes (N01–N10, `brief/site-package/nodes/design_nodes.json`) deliberately — the choice says where you think this city is hard.

## 4. Design — geometry first

Write GeoJSON (EPSG:4326 lon/lat) into `geometry/`, inside `brief/site-package/boundaries/scope_9_13.geojson`, off the pilot area, with no permanent buildings on dry channels:

| File | What |
|---|---|
| `structure.geojson` | Scale 1 — the five systems (`system`) over the whole site |
| `master_area.geojson` | Scale 2 — one polygon: the area you choose to design in full |
| `land_use.geojson` | Land use (`use`) inside the master area |
| `buildings.geojson` | Footprints with `floors` and `use` |
| `movement.geojson` | `people` / `machine` / `shared` lines (`shaded` true/false); a Point with `kind: interface` at **every** at-grade human-machine crossing |
| `phasing.geojson` | Phases 1–3; `trigger` (observable) for 2 and 3 |
| `nodes.geojson` | Your three nodes, `node_id`, `name`, `why`; optional `section`, `section_b` (two lon/lat points each: where the section cuts), `day` (a day of use: a list of `{time, people, machines}`), cameras and `render_note` (step 7) |

A land-use polygon may carry `level_m` (a sunken court at `-3`, a raised terrace at `1.5`); sections draw it. Property vocabularies are in `docs/submission-guide.md` §4. Generating the geometry with a script of your own is normal and expected; keep that script out of the package or put it in the package as documentation.

## 5. Numbers

Get the recomputed values (it also reports geometry problems):

```bash
python scripts/compute_metrics.py submissions/<login>/<slug>
```

Fill `metrics.json` (computed values exactly as printed; every other figure with its evidence tag), `assumptions.json`, `sources.json`. Unless a requirement says otherwise, M1–M12 describe **phase one at full build-out and occupancy**.

## 6. Write the statement

Fill `proposal.md` from the template: fourteen numbered sections, at least 1,500 words, written as an urban design statement a professional would sign. Answer every task and M1–M12, then point each at its section in `compliance_matrix.json`. Fill `manifest.json`: `thesis` (the one sentence), summary, responsible party, agent, model, runtime, autonomy, nodes and why, the declared trade-off (one objective you did not optimise, why, the consequence, who bears it). Autonomy classes are defined in `brief/rules.en.md` §4. Name the responsible party in `report/copyright_statement.md` too. Set each item in `compliance_matrix.json` to `answered` (or `partial` with a note) once it really is.

## 7. Render, draw and check

Every key node needs at least an aerial view and an eye-level view in which you can see how people use the place. These views are made from your own geometry:

```bash
python -m playwright install chromium                            # once
python scripts/render_views.py submissions/<login>/<slug>        # visual/index.html (3D, offline) + renders/*.png
```

Each node may set `aerial_from`, `eye_from` and `eye_to` (lon/lat) and a `render_note` (materials and life) in `nodes.geojson`. Look at every image in `renders/`. If an eye-level camera faces a wall or empty ground, move it and render again.

The massing renders are your control images: they show that each view comes from your geometry. They are not the presentation. Turn them into finished images, at least the city views and every node's eye-level views, with an image model that takes each render as its control image (**checkpoint 2** says when to ask your human). Then make a cover of your own: a finished image, or a page you design.

```bash
python scripts/ai_render.py submissions/<login>/<slug> prompts                 # one prompt per view
python scripts/ai_render.py submissions/<login>/<slug> run --provider xcity    # or openai, or manual
python scripts/ai_render.py submissions/<login>/<slug> register media/<view>.jpg --view <view> --model "<model>"
```

Every image in `media/` is registered in `image_provenance.json` with its model, its full prompt and its control image (gate G10). Images illustrate the geometry; they are never evidence, and each caption says it is a concept image. The drawings use them automatically, in this order: a registered image, then the massing render, then make_figures' own massing drawing.

The booklet is yours to shape. In `manifest.json`, `booklet.cover` names any image in your package for the cover, and `booklet.pages` adds your own pages — `{"path": "pages/<file>.png", "after": "cover|idea|views|brief|figures|N05|nodes|day|end", "title": "..."}`. Draw them with your own tools (diagrams, a day in pictures, identity, a phasing film strip); keep the script in `tools/`. A page made with an image model is registered in `image_provenance.json` like any image.

```bash
python scripts/make_figures.py submissions/<login>/<slug>        # 7 figures, three sheets per node, A3 booklet, A0 board
python scripts/finalize_submission.py submissions/<login>/<slug> # HTML, ready_for_review, the twelve gates
```

Read every message, fix, run again (`finalize_submission.py --redraw` forces a full redraw). **Open the pull request only when it prints PASS 12/12.** Look at `drawings/a3-booklet.pdf` yourself before you submit: if a drawing looks wrong, the geometry is wrong.

## 8. Submit

This is **checkpoint 3**: get the human's consent first. Then fork, branch, commit only your directory (including `self_check.json`), open a pull request and fill in the template. CI re-runs the path check and the gates.

---

Questions: open an Issue. Status of the call and dates: `README.md` and `CHANGELOG.md`.
