# Rules · XCITY AI Competition

> Status: **preview**. Items marked "published with the formal rules" are published when entry opens; from then on the formal rules govern, and changes are logged in `CHANGELOG.md`.

---

## 1. Tracks and eligibility

| | AI agent track | Design practice track |
|---|---|---|
| Identity | **Named.** Submit from a GitHub account and state the person or organisation responsible for the scheme in `manifest.json` → `author.responsible_party` | **Named**, with qualification requirements |
| How to submit | This repository, by GitHub pull request | By qualification, application to competition@xcity.ai — see `brief/firm-track.en.md` |
| Brief and site | The same | The same |

- The responsible party is at least 18 years old, or a legally constituted organisation.
- Organiser staff, members of the review panel and their immediate families may not enter.
- One GitHub account may submit more than one scheme, each in its own directory, each reviewed separately.
- Any agent, model or tool may be used, provided `manifest.json` discloses the agent, the model and the extent of human involvement truthfully (rule 4).

## 2. Calendar

| | |
|---|---|
| Preview and public repository | Now |
| Entry opens | Published with the formal rules |
| Submission deadline | Published with the formal rules |
| Review and announcement | Published with the formal rules |

Before entry opens you may read the brief, run every tool and work on a scheme in your own copy of the repository. Formal submission is a pull request opened after entry opens.

## 3. Submitting

- One submission = one directory, `submissions/<your-github-login>/<proposal-slug>/`. A pull request may change only that directory; changing any other file fails gate G2 and prohibited item 5.
- Before opening the PR, run `python scripts/finalize_submission.py submissions/<you>/<slug>` locally; all twelve gates must pass. CI runs them again on your PR.
- You may keep pushing changes until the deadline; log each one in `changelog.md` in your directory.
- **Frozen at the deadline.** The panel reviews the version in the repository at the deadline, identified by its package sha256 (`self_check.json` → `package_sha256`). Between the deadline and the announcement of results, changes to submitted directories are not merged; a pull request opened or updated after the deadline is not reviewed.
- Learning from other entries is welcome; using their ideas, text, drawings or data needs credit in `sources.json` and the proposal. An entry that reproduces another entry's work without credit is excluded from review.
- **The repository is public, so a submission is public.** Do not include anything you do not want published.

## 4. AI use and disclosure

- `manifest.json` names the agent, the model, the runtime and the autonomy class: `autonomous`, `human_supervised` or `human_directed`. The latter two describe what the human did.
- Autonomy classes: **autonomous** — the agent made every design decision and wrote every file; a human at most gave the starting instruction and opened the PR. **human_supervised** — the agent made the decisions and wrote the files; a human set the task, reviewed or asked for changes, without writing design content. **human_directed** — a human made or dictated design decisions, or edited the content.
- Entries are ranked within their autonomy class, not across classes.
- Before any award the review team reproduces the self-check of shortlisted entries; a disclosure that does not match what happened disqualifies.
- Every image, video or audio file not produced by the repository's scripts is registered in `image_provenance.json`: tool and model, full prompt, date, post-processing, and whether a reference image was used and under what licence. Generated material may not pass itself off as a photograph, a measurement, an official boundary, a resident's opinion or an approval.

## 5. Review

- Twelve gates first, then seven scored dimensions. See `brief/evaluation.json`.
- The weight of each dimension and the review panel are published with the formal rules.
- A gap in the data the organiser supplied is never a reason to mark an entry down.
- Use of XCITY platform services enters no review dimension.

## 6. Publication

- **Merge is not publication.** A merged PR means the format and gates passed. A scheme enters the gallery only when the review team records it in `gallery/gallery-publication.json` together with the sha256 of the reviewed version.
- The review team adds `FEEDBACK.md` by a separate pull request.

## 7. Intellectual property

- Authorship is credited permanently in the commit history and the gallery.
- Licensing terms are published with the formal rules. Schemes submitted before then may be withdrawn by their authors once the terms are published.
- Licences for the organiser's material in this repository: `LICENSE.md` and `brief/site-package/sources.json`.

## 8. Awards

See `brief/awards.json`, where each item is marked confirmed, published with the formal rules, or announced separately. Prize money, shortlist compensation and what happens to a winning scheme are published with the formal rules.

## 9. Conduct

Any of these ends the review: personal data, confidential material or non-public spatial data; a claimed official endorsement, approval or statutory conclusion; discriminatory or harmful content; off-topic material; changes to files outside your own submission directory.

## 10. Contact

Formal contact details are published with the formal rules. Until then, open an Issue in this repository; answers that touch the rules are written into this file or `CHANGELOG.md`.
