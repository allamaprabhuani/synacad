# SynaCAD

An AI design partner bound by the rules of mechanics: describe a part, sketch it, or photograph a broken one — the agent builds the CAD with you and emits a manufacturer-ready package; every number is computed by a validated solver, never invented.

**Landing page:** https://allamaprabhuani.github.io/synacad/

**Status:** Currently in development. Open-source, MIT-licensed.

---

## What this repo is

Right now, this repository hosts the project's landing page. The agent's source code will be released here as v1.0 ships.

## Roadmap

- **M1–3** — Intake layer (STEP/STL parsing, photo-to-CAD reconstruction, conversational CAD, feature extraction). Open-sourcing the underlying classical sizing tools.
- **M4–6** — Sizing engine wired in: LLM dispatcher with constraint enforcement before emission.
- **M7–9** — Inverse parametric design layer with Pareto-front optimisation. ASME Y14.5 GD&T generation.
- **M10–12** — Manufacturing handoff. Public v1.0 with four worked examples — a kitchen-chair clip rebuilt from a photo, a stress bracket, a fatigue lug, a pressure-vessel section.

## Built on

- [BJSFM](https://github.com/allamaprabhuani/bjsfm) — Lekhnitskii anisotropic stress-around-hole solver, MIT-licensed.
- A GPU-native, end-to-end-differentiable phase-field fracture solver in PyTorch (~10× faster than reference codes; validated against Akantu, FEniCSx, COMSOL, PhaseFieldX).
- A library of classical structural-analysis tools (lug strength, Cozzone plastic-bending, fastener load-transfer, ABD matrices, column buckling) shipped commercially through Aeroknacks India Ltd.

## Contact

- Email: allamaprabhuani@gmail.com
- Author: Allamaprabhu S Ani — Doctoral researcher, City, St George's, University of London — https://allamaprabhuani.github.io/

## Licence

MIT.
