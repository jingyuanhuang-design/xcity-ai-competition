# Visual guide

> A brief that demands drawings must supply a way to make them.

The competition page asks for a city people can see, not a stack of data layers. Every key node needs **at least one aerial view and one eye-level view in which you can see how people use the place**, plus a plan or section. Sequences, day and night, video and interactive 3D are encouraged. Dense text, mechanical diagrams or raw GIS layers do not count as the final presentation.

## 1. The image pipeline

| Step | Tool | Output | Needs |
|---|---|---|---|
| 1. 3D scene | `scripts/make_scene.py` (run by step 2) | `visual/index.html`: an offline three.js scene of your geometry on the real terrain, with sun, trees, people, robots and vehicles generated from it | Python only |
| 2. Massing renders | `scripts/render_views.py` | `renders/<view>.png` for the whole master area, the city, and each node (aerial, eye level by day, and evening or night); `renders/stamp.json` | Playwright + Chromium (software WebGL, no GPU) |
| 3. Finished images (expected) | `scripts/ai_render.py` | `media/<view>.jpg`, registered in `image_provenance.json` with model, full prompt and control image | The agent's own image tool first; otherwise any tool the human uses by hand (ChatGPT, Gemini, Midjourney, Stable Diffusion), XCITY Studio, or an API key of their own |
| 4. Drawings | `scripts/make_figures.py` | Seven figures, node sheets, A3 booklet, A0 board | Python only |

The drawings pick up the best image of each view automatically: a registered finished image, otherwise the massing render, otherwise make_figures' own massing drawing.

**Make finished images whenever you can.** The massing renders prove that the views come from the geometry; the finished images show the place to people, and the cover, the gallery card and the node sheets use them. If the agent can generate images itself, it does so without stopping to ask. An entrant with no image tool at all still passes the gates with massing renders and is not marked down for the tool it lacked, but its pages read as a model, not a city.

## 2. Cameras

`render_views.py` places the cameras itself: the master aerial frames everything you built, the city views frame your homes and shops, and the node aerials frame the buildings in each node. To control them, add to a node in `nodes.geojson`:

| Property | |
|---|---|
| `aerial_from` | `[lon, lat]`: the aerial camera looks from this direction |
| `eye_from`, `eye_to` | `[lon, lat]`: an eye-level camera at 1.6 m and the point it looks at. Stand where people are, not inside a building and not on empty ground |
| `render_note` | One or two sentences on materials and life, used in the image prompt |

`manifest.json` may carry `render_note` (the whole city), `render_rules` (rules every image must keep, such as "no private cars") and `scene_seed` (an integer: another arrangement of trees, people and vehicles; the same package always gives the same scene on any machine). **Look at every render.** If a camera faces a wall or bare ground, move it and render again.

## 3. Finished images

```bash
python scripts/ai_render.py <package> prompts                    # renders/prompts.json: one prompt per view
python scripts/ai_render.py <package> run --provider xcity       # XCITY Studio (billed to your XCITY balance, once it opens)
python scripts/ai_render.py <package> run --provider openai      # your own OPENAI_API_KEY, at OpenAI's prices
python scripts/ai_render.py <package> register media/N10-eye-day.jpg --view N10-eye-day --model "..."   # made by hand
```

**Any image tool works.** If your runtime generates images itself, that comes first: no handoff and no cost to your human. `run` automates two services; for every other tool, give it the control image and the prompt from `renders/prompts.json`, save the result under `media/`, and `register` it. When your human makes the images by hand, hand them each control image with a prompt ready to paste. The panel judges agreement with the geometry, not the tool. The example package happens to use ChatGPT by hand; that is one choice, not a requirement.

Each prompt asks the model to keep the control image's camera, footprints, heights, streets and trees, and to change only materials, light and life. An agent must ask its human before spending money (AGENTS.md, checkpoint 2). Keys stay in the environment or in `~/.xcity/`, never in the repository.

## 4. What make_figures.py draws

| File | Content |
|---|---|
| `fig-01-structure.png` | Whole site: the six systems with their recomputed areas, pilot area, channels, master area, nodes |
| `fig-02-master-plan.png` | Master area: land use, figure-ground, networks, place names, overall dimensions, nodes |
| `fig-03-land-use-density.png` | Buildings by floors; land use areas; coverage, FAR, open space recomputed |
| `fig-04-movement.png` | People, machine and shared networks; every interface numbered |
| `fig-05-open-space-water.png` | Open space, shaded and unshaded walking, channels and flood corridors |
| `fig-06-phasing.png` | Phases 1–3 with areas and triggers |
| `fig-07-metrics.png` | Every declared metric, its evidence tag, and the recomputed value where there is one |
| `node-<id>-plan.png`, `-aerial.png`, `-eye.png` | For each node: the plan, and the best aerial and eye-level image |
| `drawings/a3-booklet.pdf` | The cover (your choice of image), the idea (thesis and the three scales on one page), the city views, how the scheme answers the brief, the seven figures, three sheets per node — views; plan with dimensions and numbers plus sections and street sections at true scale; a day of use with people and machines — day to night at eye level, your own pages, and assumptions, sources and AI disclosure |
| `drawings/a0-board.pdf` | One A0 board |

Every sheet carries a title, sources, the script version and a hash of its inputs, which include the renders and the registered images. The drawings say nothing your data does not.

**Make the booklet yours.** The required pages are a floor. `manifest.booklet.cover` picks the cover; `manifest.booklet.pages` adds pages you draw yourself (see `docs/submission-guide.md` §5). In `nodes.geojson`, `section` / `section_b` place the cuts and `day` writes the day of use; a land use with `level_m` is drawn at its level. The example's identity page comes from its own `tools/make_pages.py`.

## 5. Registering media

Every file under `media/` is registered in `image_provenance.json` (template: `templates/image_provenance.example.json`). `ai_render.py` does this for you.

| Field | |
|---|---|
| `path` | `media/...` |
| `node_id`, `view` | e.g. `N05`, `aerial` / `eye_level` / `other` |
| `model` | Tool or model and version |
| `prompt` | The full prompt, not shortened |
| `generated_at` | Date |
| `post_processing` | `none`, `retouch` or `composite` (+ `post_processing_note`) |
| `reference_images` | `none_text_only_prompt`, `own_work` or `third_party`; the last two need `reference_images_note` |
| `control_image` | `renders/<view>.png` the image was made from; gate G10 checks it exists and is current |
| `caption` | Must make clear it is a concept image that explains the geometry, not evidence |

**Rules.** Generated material may not pass itself off as a photograph, a measurement, an official boundary, a resident's opinion or an approval. Video carries a poster, captions and a transcript; audio a transcript; nothing autoplays. A render is judged on agreement with the submitted geometry — heights, positions, orientation — not on how good it looks. A render that contradicts the geometry costs points rather than earning them. **Which image tool you used is not visible to the panel and earns nothing.**

## 6. Interactive pages

`visual/index.html` is written for you: open it in any browser to orbit the scene and switch views. Anything else interactive goes under `media/`. Pages must work offline (gate G5): no CDN, no map tiles, no web fonts, no API calls, no iframes. Bundle any library you use into the package.

## 7. Cost

Every required output is free and offline. Finished images need not cost anything either: an agent's built-in image tool, or a free tier used by hand, is enough. Paying earns no points, and an image that disagrees with the geometry costs points. Your XCITY account comes with a KWH balance that can be spent on images.
