# Reiser Lab Documentation

Source for the [Reiser Lab documentation site](https://leburnett.github.io/reiser-documentation):
how to run experiments on the G3 and G4 LED arena setups at HHMI Janelia.

**Version** README v1 · **Status** active · **Last verified** not yet verified

## What this does

- Builds a Quarto website documenting the freely-walking, electrophysiology and tethered
  flight rigs — rig specs, installation, protocols, analysis and troubleshooting.
- Publishes to GitHub Pages automatically on every push to `main`.
- Hosts the pattern and protocol reference pages that the
  [freely-walking-optomotor](https://github.com/leburnett/freely-walking-optomotor)
  repository generates.

**You will need:** [Quarto](https://quarto.org) installed locally to preview. Nothing else —
there is no data dependency and no rig required.

## Quick start

```bash
git clone https://github.com/leburnett/reiser-documentation.git
cd reiser-documentation
quarto preview --port 4321
```

Opens the site at `http://localhost:4321` and live-reloads as you edit. To build once
without serving:

```bash
quarto render --to html
```

Output goes to `_site/`, which is not version-controlled.

## Repository map

| Path | Contents |
|---|---|
| `index.qmd`, `resources.qmd` | Landing page and resources |
| `Freely-walking/` | Freely-walking optomotor docs — 17 hand-written pages plus 100 generated ones |
| `Ephys/` | G4 electrophysiology: DS probe and nested RF protocols, 22 pages |
| `Tethered/` | Tethered flight rig |
| `assets/` | Images, GIFs and favicons (~500 files) |
| `_quarto.yml` | Site config: navbar, per-section sidebars, filters |
| `theme-light.scss`, `theme-dark.scss` | Light and dark themes |
| `skip-gifs-in-pdf.lua` | Pandoc filter: substitutes still frames for GIFs in PDF output |
| `_extensions/` | Quarto extensions, including the page-timestamp filter |
| `.github/workflows/` | `ci.yml` renders on PRs; `pages.yml` deploys `main` to Pages |

## Editing the site

**Do not hand-edit the generated pages.** `Freely-walking/patterns/` (65 pages) and
`Freely-walking/protocols/` (35 pages) are written by the `docs_generator` package in the
freely-walking-optomotor repository, from the pattern `.mat` files and protocol `.m` files
themselves. Regenerate them there instead:

```bash
# in the freely-walking-optomotor repo
cd python/freely-walking-python
pixi run gen-pattern-docs
pixi run gen-protocol-docs
```

Everything else is hand-written `.qmd` and safe to edit directly.

**Adding a page:** create the `.qmd` in the relevant section directory and add it to that
section's `sidebar.contents` in `_quarto.yml`. Individual pattern and protocol pages are
deliberately *not* in the sidebar — they are reached from the index tables.

**Deployment:** merge to `main`; `pages.yml` renders and publishes. No manual step.

## Conventions & gotchas

- The site renders to both HTML and PDF. LaTeX cannot embed GIFs, so animated content is
  wrapped in `.content-visible when-format="html"` blocks with a still-frame fallback for
  PDF — `skip-gifs-in-pdf.lua` enforces this.
- Markdown tables break if rows are separated by blank lines; keep table rows consecutive.
- Rendering leaves LaTeX intermediates and `*_files/mediabag/` directories behind; both are
  gitignored.
- Some pages reference rig paths (`C:\matlabroot\…`) and the group drive
  (`/Volumes/reiserlab/…`). These are the same on every machine of that kind and are
  intentional; they are not personal paths.

## Related

| Repo | Documents |
|---|---|
| [freely-walking-optomotor](https://github.com/leburnett/freely-walking-optomotor) | The `Freely-walking/` section; also generates its pattern and protocol pages |
| [nested_RF_stimulus](https://github.com/leburnett/nested_RF_stimulus) | The nested RF protocol pages under `Ephys/` |
| [DS_probe_protocol](https://github.com/leburnett/DS_probe_protocol) | The DS probe protocol pages under `Ephys/` |
| [G4_Display_Tools](https://github.com/leburnett/G4_Display_Tools) | Arena control software the docs assume |
| [Modular LED Display](https://reiserlab.github.io/Modular-LED-Display/G4/) | The G4 hardware itself |

## Contact

Laura Burnett, Reiser Lab, HHMI Janelia Research Campus.
