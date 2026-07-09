# Social Spike WordPress Proposal System v1.2.3

This is the clean replacement package for the WordPress service-business proposal system.

## Why this package is lean

The original system carried very large embedded HTML, PDF, logo, and screenshot assets. Those belong in GitHub, not in Claude project knowledge. This package keeps the reusable thinking, rules, scripts, schema, and QA in the zip, while the heavy production assets stay in:

`https://github.com/Socialspike/Socialspike-assets`

## What changed from the uploaded project

- Corrected the project identity. This is the WordPress proposal system, not the SEO proposal engine.
- Standardized filenames.
- Removed fake/broken PDF from the package.
- Moved heavy HTML/PDF handling to GitHub asset sync.
- Set the proposal as a deliberate 12-page structure.
- Added real build and validation scripts.
- Added scorecard rubric.
- Added variable schema.
- Added asset manifest.
- Added visual improvement notes.
- Added a clean system guide.
- Removed large base64 screenshot/logo docs from project knowledge and replaced them with asset rules.

## First run

From this folder:

```bash
python scripts/sync_wp_assets.py
python scripts/validate_wp_proposal.py --check-assets
python scripts/build_wp_proposal.py --variables config/example_variables.json --output output/example_proposal.html
python scripts/validate_wp_proposal.py --html output/example_proposal.html
```

To render a PDF, install Playwright locally:

```bash
pip install playwright
python -m playwright install chromium
python scripts/build_wp_proposal.py --variables config/example_variables.json --output output/example_proposal.html --pdf output/example_proposal.pdf
python scripts/validate_wp_proposal.py --html output/example_proposal.html --pdf output/example_proposal.pdf --target-pages 12
```

### Font setup

`wp_proposal_v1.html` embeds League Spartan directly in the file as base64 `@font-face` data, so no font install is required to render a correct PDF. Playwright renders the embedded font automatically.

A project-level `package.json` (with `@fontsource/league-spartan`) is included as a safety-net dependency for any workflow step that needs the font files on disk outside the template itself (e.g. building a new template variant from scratch). It is not required for standard proposal rendering. If you need it:

```bash
npm install
```

Do not install League Spartan globally. Always use the project-local `npm install` above so every fresh session behaves identically.

## Final package recommendation

Upload this lean package into project knowledge. Keep the GitHub repo as the asset source for the production HTML and PDF render.

## v1.2.1 expanded asset note

This package includes local reference assets in `/assets`:

- `wp_proposal_v1_reference_render.pdf`
- `wp_proposal_v1_reference_pages/`
- `wp_proposal_v1_contact_sheet.jpg`

The editable production HTML template remains `assets/wp_proposal_v1.html`, synced from GitHub using `scripts/sync_wp_assets.py`. If that file is not present, run the sync script or manually place the GitHub HTML into `/assets`.


## v1.2.3 render QA fix

This version keeps the strong 12-page proposal system and adds the cleanup found during the full render review.

Main updates:

- Page 11 portfolio continuation numbering is now enforced.
- Page 3 wording is simplified for buyers.
- Page 3 center label is changed to Local Search Signals.
- Page 8 heading is changed to What This Build Gives You.
- Page 9 industry match line must use a pipe or colon instead of an em dash.
- Page 6 deliverable copy is tightened by system rule.
- Page 7 bottom cards now need a distinct job, not a repeat of the timeline.
- Proof claims must be approved before live use.
- Validator now checks duplicate section numbers, proof status, raw em dashes, page density warnings, and portfolio numbering.

After syncing the GitHub HTML, run:

```bash
python scripts/patch_wp_template_v122.py --template assets/wp_proposal_v1.html --write
python scripts/validate_wp_proposal.py --html assets/wp_proposal_v1.html --proof config/example_variables.json
```

Then build and render your test proposal again.


## v1.2.3 final template fix

This version applies the final cleanup found after the proof render review.

- Page 3 center diagram now reads Local Search Signals instead of Google Local Ranking Algorithm.
- README text has no raw em dashes.
- The live template, proof render, package files, and validation rules are aligned.
- The old temporary merged file is not used. The source of truth is wp_proposal_v1.html.
