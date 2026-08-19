# Targets

One folder per target, one slug per folder. Prefer this shape:

- `README.md`: one-page status, target facts, strongest leads, next action.
- `THREAT_MODEL.md`: from `../THREAT_MODEL_TEMPLATE.md`.
- `analysis/`: traces, experiments, scratch scripts, `known-fixes.md`.
- `findings/`: evidence-backed candidates, reports, disclosure drafts.
- `pocs/` or `tools/`: marker-only repros, harnesses, probes.
- `artifacts/`: binaries, packages, logs, captures. Not loaded by default.
