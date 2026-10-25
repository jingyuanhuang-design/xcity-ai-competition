# Changelog

Changes to the brief, the site package, the rules and the tools — newest first. Entrants: if a change affects your scheme, note it in your own `changelog.md`.

## 2026-10-25 — practice track, map and wording

- Design practice track: its own page (`practice.html`); an application form (`templates/firm-application-form.docx`, one page in English, Chinese and Spanish) as the first page of the application PDF; a questions-and-answers section — answers are published in the repository, the same for every applicant (`brief/firm-track.*.md`, section 4).
- Wording: "pilot area" for the lead zone. File and field names are unchanged (`brief/site-package/lead-zone/`).
- Indicative systems: a fifth living point marks the organiser's planned living area; its position is approximate (`zoning/indicative_systems_9_13.json`).
- Competition page: a language list (English by default), a centred map with distance arrows in proportion to each road's distance and a 10 km scale bar.

## 2026-10-25 — finished images

- Finished images are now expected, not optional. An agent that can generate images makes them itself, over its massing renders, without stopping to ask; otherwise its human makes them with any tool they already use, from control images and prompts the agent prepares. Massing renders only is the last resort. Each image is captioned as a concept image (AGENTS.md checkpoint 2, `docs/visual-guide.md`).
- The self-check notes an entry with no finished images; the gates are unchanged.

## 2026-10-24 — preview published

- Repository opened as a preview of the XCITY AI Competition: parcels 9 and 13, 1,656 km².
- Brief (zh / en), design requirements, rules, design practice track, agent taskbook, evaluation (12 gates, 7 dimensions), scenarios, awards.
- Site package: exact parcel boundaries, lead zone, roads, DEM (60 m), hillshade, DEM-derived channels, terrain summary, indicative systems, ten key nodes.
- Tools: scaffold, make_figures (7 figures, node massing views, A3 booklet, A0 board), render_proposal_html, self_check (12 gates), finalize, CI path check.
- Renders: scripts/make_scene.py (offline three.js scene of the scheme on the real terrain, with trees, people, robots and shuttles), scripts/render_views.py (aerial and eye-level views of the master area, the city and each node, by day and by evening or night) and scripts/ai_render.py (prompts, finished images through XCITY Studio or the entrant's own tool, registration with a control image). Gate G10 checks that the scene, the renders and every registered image are current.
- Drawings are image-led: the booklet opens with the city seen whole, then the city views, the seven figures, one sheet per node, and day to night at eye level.
- Agents stop and ask their human three times: the idea and the nodes (two or three directions to choose from), the image tool, and consent before the pull request; after submitting they keep returning, revise and log each round.
- Deeper node drawings: each node now has three sheets — views; a plan with overall dimensions, street widths and numbered interfaces, sections at true scale (`section`, `section_b`) and a cut across each kind of street; and a day of use (`day`) with the people, robots and shuttles of the 3D scene.
- The booklet opens with the idea (`manifest.thesis`) and a page showing where every mandatory requirement and agent task is answered. Entrants choose the cover (`booklet.cover`) and add their own pages (`booklet.pages`).
- Entries are frozen at the deadline: the version in the repository then (its package sha256) is the one reviewed. Borrowing from other entries needs credit.
- Design practice track: a call for qualifications (`brief/firm-track.*.md`, in English, Spanish and Chinese) — apply to competition@xcity.ai.
- The site is in English, Spanish and Chinese, and opens in the visitor's browser language. The scheme page is a workspace: read the statement, browse every file, check the evidence behind each figure, and see each image beside the render it was made from.
- Example package: submissions/EXAMPLE-agent/sample-scheme — "Terrace Oasis", a city of about 41,000 people, with finished images made from its renders.
- Entry dates, review panel, dimension weights and licensing terms: published with the formal rules.
