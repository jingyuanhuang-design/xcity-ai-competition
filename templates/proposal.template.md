# {{title}}

> XCITY AI Competition · Parcels 9 and 13 · submissions/{{github}}/{{slug}}
> Write this as an urban design statement a professional would sign — not as a description of your files.
> Keep the fourteen numbered headings exactly as they are (`## 1.` … `## 14.`): compliance_matrix.json points at them and gate G6 checks they exist. You may add `###` sub-headings freely. Delete every line that starts with `>` before you submit.
> Embed figures with paths relative to the package, e.g. `![Structure](figures/fig-01-structure.png)`.

## 1. Position

> agent.1. The idea of this city in a paragraph. A naming system for the city, its settlements and districts; logo direction (described and shown); a visual standard — type, colour, signage logic. What you believe this city is for, in one sentence a resident could repeat.

## 2. Site reading

> Read the site before you design it: water, slope, the Pie de Palo range, the Zonda, seismic risk, the dry channels, the pilot area, the 27.6 km to the nearest road. Which of these decided your structure, and how? A scheme that would look the same on another site scores low on D1.

![Structure](figures/fig-01-structure.png)

## 3. Energy and compute

> agent.2 · M1 · M2 · M4. Where generation, storage, substation and compute sit, and why. Hourly carbon-free matching as a method (physical or contractual), what happens at night, the grid capacity you assumed, where the waste heat goes and who receives it. Cooling type, WUE and PUE together.

## 4. Water

> agent.3 · M3 · M4 · M5. A water balance: sources, uses (domestic, compute cooling, agriculture, landscape, industry — they add up to the total), losses, reuse. What is irrigated with what. What stops first when water is 30% short, in order, and what happens in the city at each step.

![Open space and water](figures/fig-05-open-space-water.png)

## 5. Human and machine

> agent.4 · M6 · M7. Two networks — people, and machines plus goods. Every at-grade interface is a Point in geometry/movement.geojson; say how each kind is made safe. Separated, mixed or time-shared, where, and who decides. Kerb, loading, charging, storage.

![Movement](figures/fig-04-movement.png)

## 6. Programme and production

> agent.5 · M12. Programme by use and share. Jobs by type and by phase, with the basis. Phase one: who is here, and do jobs, residents and dwellings reconcile? What is produced on site — including the agrivoltaic fields — and for whom. No jobs figure without a skills mix and a named trainer.

## 7. Urban form

> agent.6. Three scales. (1) The whole site: where the five systems sit. (2) Your master design area: why it is there — write down how water, slope, wind, the way out and the pilot area pushed you there — and its blocks, massing, heights and density (recomputed from your geometry). (3) Public realm under desert conditions: shade, wind, water, ground. How the scheme uses parcel 9 (with the range and its eastern wing) and parcel 13 (with the pilot area).

![Master plan](figures/fig-02-master-plan.png)

![Land use and density](figures/fig-03-land-use-density.png)

## 8. Governance and data

> agent.7 · M8 · M9. What data the city produces and who may read it. What the public can audit, through what instrument, how often, and who checks independently. Who controls the compute asset and what happens if that operator leaves. At least one named failure mode and its mitigation.

## 9. Phasing

> agent.8 · M10 · M11. Three phases on the site. Phase one stands on its own — its own production, logistics and services. Observable triggers for phases two and three. At least three phase-one decisions that cannot be changed later, and why that is acceptable. The long-term size you propose, and how many settlements.

![Phasing](figures/fig-06-phasing.png)

## 10. Key nodes

> Three of the ten (brief/site-package/nodes/design_nodes.json), each to detailed design: a plan or section, an aerial view, an eye-level view. Say why these three. make_figures.py renders massing views from your geometry; add your own renders in media/ if you can, and register each in image_provenance.json.

### {{node_1}}

![Plan](figures/node-{{node_1}}-plan.png)
![Aerial](figures/node-{{node_1}}-aerial.png)
![Eye level](figures/node-{{node_1}}-eye.png)

### {{node_2}}

![Plan](figures/node-{{node_2}}-plan.png)
![Aerial](figures/node-{{node_2}}-aerial.png)
![Eye level](figures/node-{{node_2}}-eye.png)

### {{node_3}}

![Plan](figures/node-{{node_3}}-plan.png)
![Aerial](figures/node-{{node_3}}-aerial.png)
![Eye level](figures/node-{{node_3}}-eye.png)

## 11. Metrics and evidence

> The numbers that carry the scheme, each with its evidence tag (computed / sourced / assumed / indicative). Computed ones must match your geometry within 2% — the self-check recomputes them.

![Metrics](figures/fig-07-metrics.png)

## 12. Risks and failure modes

> Not a list of risks. Which failure is actually likely here — flood, quake, Zonda, water shortfall, the operator leaving — what the plan does when it happens, and who decides.

## 13. Declared trade-off

> One objective this scheme deliberately did not optimise, why, what follows from it, and who bears the cost. The same four answers go in manifest.json → tradeoff.

## 14. Sources, assumptions and AI disclosure

> Where the numbers came from (sources.json, assumptions.json). Which agent and model did what, and what any human did (manifest.json → agent, autonomy). Which images were generated and how (image_provenance.json).
