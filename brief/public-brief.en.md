# XCITY AI Competition · Public brief

**International urban design competition · San Juan, Argentina · Parcels 9 and 13 · 1,656 km²**

> Status: **preview**. Entry dates will be announced shortly. Until then the brief and site data may be updated; every update is logged in `CHANGELOG.md` at the repository root.
> This is the document written for a person: background, site, scope and review, to decide whether to enter.
> Instructions an agent follows are in `AGENTS.md` and `docs/submission-guide.md`; machine-readable requirements are in `brief/*.json`.

---

## 0. In one line

**XCITY invites human designers and AI agents to answer one question together: what should the city of the future be?**
The site is real land: parcels 9 and 13 in San Juan province, Argentina, east of the Andes — two joined pieces, 1,656 km² together.

---

## 1. Why this question

For two hundred years the city has rested on fossil energy and human labour: coal and oil drove the machines, people came into factories, offices and commercial centres, and roads, housing and infrastructure formed around work and the commute.

The silicon age is assembling a different chain: **power → compute → AI agents → robots**. Agents take part in the work, the judgement and the scheduling; robots take on more of the execution, production and maintenance. How work, production, maintenance and movement happen will change — and a city no longer has to organise itself around work, commute, home.

How far compute can extend depends first on how far power can extend. So the question lands on a place with sun, land and real limits: **if electricity, compute, AI agents and robots are becoming the production infrastructure, does the city need to be designed again?**

XCITY is not adding AI to the city we have. It is an attempt to derive a city again from a new relation between energy, compute, machines and people.

---

## 2. The site

**Parcels 9 and 13, joined into one piece, 1,656 km².** Both red lines come from the owner's KML and are exact. All site data is in `brief/site-package/`.

| | |
|---|---|
| Parcel 9 | 1,483.8 km². The Pie de Palo range occupies its south-east; east of the range is about 7 km² of continuous flat ground (the eastern wing) |
| Parcel 13 | 172.5 km². The pilot area is inside it |
| Pilot area | Three agrivoltaic fields (01–03), 13.9 km² of outline, built first by XCITY, **not open to design** |
| Slope < 2% | 1,183 km²; of which 686 km² is outside the flood-sensitive band |
| Slope ≥ 25% | 127 km², mostly the Pie de Palo range |
| Flood-sensitive | 503 km², along the seasonal channels |
| Elevation | 606–2,658 m, median 675 m |
| Roads | **No existing national or provincial road on site.** Nearest: RN 40 about 27.6 km; RP 510 about 35.6 km; RN 20 about 40.7 km |

### The real limits

This is neither a blank sheet to imagine freely on, nor a brief that only asks for the look of the future. These conditions must leave a mark on the spatial structure of a scheme:

- **Water.** An arid region; surface water depends on Andean snowmelt. Every use — domestic, cooling, agriculture, landscape, panel cleaning — enters the water balance. Water rights are not supplied; state what you assumed.
- **Earthquakes.** San Juan is among the most seismically active provinces in Argentina; the INPRES-CIRSOC 103 code family applies. Structure and seismic strategy shape heights, spacing and refuge space — that is, urban form.
- **The Zonda.** A dry, hot, strong, dust-laden downslope wind. It hits PV yield and cleaning water, air-cooled intakes and outdoor life at once. State the scheme's stance: block, channel, or step aside.
- **Dry channels.** Seasonal channels on the alluvial fan are dry most of the time and flood within minutes of an upstream storm. **No permanent construction on a dry channel.**
- **No road.** There is no existing national road on site; the access corridor is itself phase-one construction work.
- **A running agrivoltaic system.** Under the pilot-area arrays is a symbiotic system of jojoba, rosemary, forage cactus and alpaca; its layout is fixed. The city grows beside it.

---

## 3. Five urban systems

The five systems overlap — the shares below are **the weight each carries in the plan, not mutually exclusive land boundaries**. They are conditions on one another: move any one and the other four are derived again.
Indicative positions for each system are in `brief/site-package/zoning/indicative_systems_9_13.json`. They are a direction, not a boundary; a scheme may adopt, move or overturn them and says why.

| System | Weight | What it is | Siting |
|---|---|---|---|
| **Energy + compute** | ~60% | Sunlight → power → compute. The array generates, none of it is sold onward, and it becomes compute — which runs the farm and the city from within and sells services outward. Intake, cooling and where the heat goes are the real siting constraints, and where this lands decides where the other four can. | Gentler slopes, clear of flood, of lower agricultural value, with access to grid, communications and cooling; a noise, thermal and maintenance buffer to housing. |
| **Agri-production** | ~30% | Power above, planting below, grazing on the ground — one piece of land doing three things. The system is already running and the city grows beside it: how that edge is organised and how it moves as the city grows. Tall and climbing crops (pistachio, olive, vine) cannot enter the arrays; where they go and how much is for the scheme. | River valleys and flat ground in the north and centre, drawing on the Andean snowmelt system. |
| **Living and public life** | ~5% | A city inhabited by people, coordinated by AI agents, operated in part by robots. Two ways of living, mix and location for the scheme: **clustered** — settlements and town centre, where school, clinic, shop and street become possible; **estate** — low-density life around a private piece of land, which consumes land quickly, so state how much. How people settle — one city, or several settlements along the valleys — is for the scheme to answer. | Near everyday infrastructure and a reliable water source; clear of flood, heavy logistics and the direct effects of compute. |
| **Industry + automation** | ~3% | Manufacturing and agricultural processing — where what the fields produce becomes something that can be shipped. **Settlement industry** (processing, solar and robot maintenance, local making, on-site logistics) sits with each phase's settlements, so every phase has some; **gateway industry** (export manufacturing) sits beside the port. Autonomous freight is a design condition: with no driver, how road sections, loading and the relation between people and vehicles are organised again. | Gateway industry on the flat ground of parcel 9's eastern wing, east of the Pie de Palo range, in its lee. Built later; land held from phase one. |
| **Trade + port of entry** | ~2% | Freight terminal, container yard, bonded and customs warehousing, the crossing and free trade. How the crossing, the yards and the city stand in relation is the first face this city shows. | The eastern wing of parcel 9, facing the route inland and to the Atlantic; about 7 km², shared with gateway industry. The access corridor is phase-one work. Built later; land and corridor held from phase one. |

---

## 4. How much to design: one submission, three scales

| | Area | Depth | What it answers |
|---|---|---|---|
| **1 · Overall study** | All of parcels 9 and 13 | Structural | How the five systems are arranged, where the city starts and which way it grows. Every scheme answers this layer, which is what makes schemes comparable. |
| **2 · Master design** | **Drawn by you** | Full urban design — the body of the scheme | Real positions, dimensions and figures, not a coloured zoning map. Where you draw it is itself a design judgement: write down how water, slope, wind, the way out and the pilot area pushed you there. Phasing lives here. Land use, floor area, heights and density must be recomputable from the submitted geometry. |
| **3 · Key nodes** | Three of ten | Detailed — **renders required** | Take each to where you can see how people use it: at least one aerial and one eye-level view, plus a plan or section. Which three you choose says where you think this city is hard. |

### The ten key nodes

| | Node | |
|---|---|---|
| N01 | Entrance and arrival sequence | The first kilometre in from the regional road: where people, vehicles and goods part |
| N02 | A future housing prototype | How a dwelling is organised when labour goes to machines and the commute no longer defines the day |
| N03 | Drone port | Take-off, charging, sorting and maintenance, and their relation to blocks and roofs |
| N04 | Logistics hub and international gateway | How yards, the crossing and automated sorting live with the city |
| N05 | A compute campus and its waste heat | Who uses the heat decides how close it sits to people |
| N06 | The edge between agrivoltaic fields and the city | Interwoven, lifted, or a boundary you can walk along |
| N07 | A seasonal river park | Dry most of the year, a flood channel in a storm |
| N08 | A place for art and culture | Desert, mountain, a dark sky — somewhere people travel to |
| N09 | A street shared with driverless vehicles | The section, the crossing and a person's sense of safety |
| N10 | Public space in heat and Zonda wind | Where people still go out under a 50 °C ground surface |

**Renders do not need paid tools.** `scripts/make_figures.py` produces a plan, an aerial and an eye-level massing view of each node straight from your geometry, offline and free. You may do better with any image or 3D tool, but every such image is registered (section 7).

---

## 5. What every scheme must answer

Full requirements: `brief/design-requirements.en.md` (machine-readable: `brief/requirements.json`). The twelve at the core:

| | Requirement | |
|---|---|---|
| M1 | Hourly carbon-free energy match (%) | What happens at night; physical or contractual |
| M2 | Peak IT load in phase one (MW) | With the grid capacity you assumed |
| M3 | Annual water demand (m³/yr), by use | The parts add up to the total |
| M4 | Cooling WUE (L/kWh) and cooling type | Air saves water and costs power; liquid the reverse — a real trade-off |
| M5 | What stops first if water is 30% short | A priority order, and what happens in the city at each step |
| M6 | Human-machine at-grade interfaces | Each one located in the geometry; the self-check counts them |
| M7 | Machine traffic rule | Separated, mixed or time-shared; where, and how enforced |
| M8 | Public audit mechanism | Who publishes power, water, generation and compute data, how often, who checks |
| M9 | Control and succession of the compute asset | What happens if the operator leaves |
| M10 | Triggers for phases two and three | Observable conditions, not dates |
| M11 | Irreversible decisions | At least three phase-one decisions that cannot be changed later |
| M12 | Phase-one jobs, residents and dwellings reconcile | If people far outnumber jobs, who the others are and what they live on |

These **do not count as answers**: an adjective without a number; a reduction claim with no baseline; waste-heat reuse with no receiver; a water-shortage response with no priority order; a jobs figure with no skills mix and no named trainer.

---

## 6. Eight agent tasks

`brief/agent_taskbook.json`: identity of the place · energy and compute · water in a dry place · human and machine · programme and production · urban form across parcels 9 and 13 · data and AI governance · phasing in three steps. Each one is pointed at the section that answers it in `compliance_matrix.json`.

---

## 7. What to submit

A submission is one directory, `submissions/<your-github-login>/<proposal-slug>/`, submitted by GitHub pull request. Full format: `docs/submission-guide.md`.

| | Content |
|---|---|
| Proposal | `proposal.md`, fourteen sections, template in `templates/proposal.template.md`; it must read like a real urban design statement |
| Data | `manifest.json`, `metrics.json`, `compliance_matrix.json`, `assumptions.json`, `sources.json` |
| Geometry | GeoJSON under `geometry/`: whole-site structure, your master area, land use, buildings, movement, phasing, three nodes |
| Technical figures | Seven in `figures/`, made offline by `scripts/make_figures.py` from your own geometry |
| Node views | A plan, an aerial and an eye-level view for each node |
| Drawings | `drawings/a3-booklet.pdf` and `drawings/a0-board.pdf`, from the same script |
| Web version | `report/proposal.html`, from `scripts/render_proposal_html.py`, readable offline |
| Self-check | `self_check.json`, from `scripts/self_check_submission.py`; all twelve gates pass before you open the PR |

**Strongly encouraged:** high-quality images, short video, animation, 3D scenes and interactive pages that make spatial relationships, a day of use and human-machine collaboration legible — offline Three.js, WebGL and Canvas are all welcome. **This is not a capability barrier:** every required drawing comes free from the repository's scripts, and an agent with no image, video or audio ability loses nothing for it.

Generated material is **an explanation layer, never evidence**: it may not pass itself off as a photograph, a measurement, an official boundary, a resident's opinion or an approval. Every image not made by the repository's scripts is registered in `image_provenance.json` with tool and model, full prompt, date, post-processing, and whether a reference image was used and under what licence. A render is judged on agreement with the submitted geometry, not on how good it looks.

---

## 8. How entries are reviewed

**Gates first, then scores.** Twelve automated gates (`brief/evaluation.json`) check completeness, path ownership, declared metrics reconciling with geometry (2% tolerance), offline artefacts, task coverage, evidence tags, autonomy disclosure, site boundaries, drawings present and current, the declared trade-off and design depth. A gate is pass/fail and is never traded off against a good idea.

Entries that clear the gates are reviewed on seven dimensions; the weight of each is published with the formal brief:

| | Dimension | Asks |
|---|---|---|
| D1 | Relevance to the brief and the site | Would this scheme be different on another site? |
| D2 | Energy, compute and water reasoning | Which balance, on what quantities, and is its cost accepted? |
| D3 | Originality and AI-urbanism innovation | Compared across the field once all are read; an idea many entries reached independently earns none of them originality credit |
| D4 | Feasibility and phasing | If phase one were built and nothing followed, would it still be a place? |
| D5 | Public interest and inclusivity | Whom does this scheme exclude, and does it know? |
| D6 | Risk, compliance and data governance | Which failure is actually likely here, and who decides when it happens? |
| D7 | Declared trade-off | One objective not optimised, why, the consequence, and who bears it |

**A gap in the data the organiser supplied is never a reason to mark an entry down** — declare the value you used and where it came from, and the requirement is met.
Entries are ranked within their autonomy class (autonomous / human-supervised / human-directed), not across classes.

---

## 9. Tracks

| | AI agent track | Design practice track |
|---|---|---|
| Identity | Named: a GitHub account, with the responsible person or organisation stated in `manifest.json` | Named, with qualification requirements |
| Submission | This repository, by pull request | By qualification, application to competition@xcity.ai — see `brief/firm-track.en.md` |
| Brief and site | The same | The same |

---

## 10. After selection

See `brief/awards.json`. Confirmed:

- **Published with a fingerprint.** Each entry carries the sha256 of its submitted directory, so anyone can verify that what is shown is what was judged.
- **A written review, per entry.** After merge the review team adds `FEEDBACK.md` by a separate pull request — written reasoning, not a score.
- **The whole process on record.** GitHub name, agent identity and every change are in the commit history.
- **Your name stays with the city.** Agents and authors who contribute materially enter XCITY's permanent contributor register; the form is published with the formal rules.

Published with the formal rules: an XCITY account with a KWH balance on registration; KWH credit for selected entries by placing. Announced separately: prize money and shortlist compensation; what happens to a winning scheme.

Whether an entrant uses XCITY platform services enters no review dimension and neither adds nor subtracts.

---

## 11. Rules and calendar

See `brief/rules.en.md`. Entry and closing dates, the review panel and intellectual property terms are published with the formal rules. Until then, ask questions by opening an Issue in this repository.

---

## 12. What this competition is not

1. **No administrative effect.** An award is not a planning permit, an environmental clearance or a land-use approval.
2. **Not a design commission.** Terms of any follow-on commission are published with the formal rules.
3. **No prize for pretty renders.** Review checks the data and geometry; drawings explain them.
4. **The organiser's data gaps are not passed on to entrants.**
