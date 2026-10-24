# lets-study-vision-AI-driven-2026

Personal study repo for the one-day course **"From Pixels to Low-Level Optimization: Computer Vision Driven by LLMs"**. Solo project — my own notes, code, and results only.

## Layout

- `docs/plan-1-day.md` — the one-day route: modules, schedule, metrics, and the transversal production analysis.
- `modules/` — study material, one folder per module. Every module has the same five folders:
  - `notebooks/` — runnable `.ipynb` files.
  - `reports/` — results, measurements, and write-ups.
  - `notes/` — scratch notes and decisions.
  - `theory/` — mathematical and conceptual deep dives.
  - `exercises/` — problem statements and my solutions.
- `modules/_template.md` — the template I use to develop each module.

## Workflow

1. Read `docs/plan-1-day.md` for the module scope and target metric.
2. Copy `modules/_template.md` into the module's `notes/` (or keep it as the module README) and fill it in.
3. Build the module in this order: `theory/` → `notebooks/` → `exercises/` → `reports/`.
4. Record every measurement in `reports/` using the same protocol (warmup, repeated runs, p50/p95, machine spec) so numbers stay comparable across modules.

## Conventions

- Documentation and code comments in English.
- No models, datasets, or generated outputs in git — see `.gitignore`.
- Relative paths only (`modules/module-01/...`), so the repo works from any machine.
