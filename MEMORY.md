# Workspace Memory

- This workspace is for responsible vulnerability research in owned labs,
  disposable VMs, local source trees, and coordinated disclosure workflows.
- Default agentic method: small threat model, one thin slice, exact evidence,
  safe verifier, novelty check, then report or park.
- The AI acts as planner, source navigator, hypothesis manager, experiment
  coordinator, critic, and scribe. The human owns scope, lab access, risk
  decisions, disclosure judgment, and final claims.
- Keep persistent context small. Prefer `README.md`, `MEMORY.md`,
  `METHODOLOGY.md`, and the current target's threat card over broad logs or
  unrelated case studies.
- Validation ladder: source proof, local model, instrumentation, marker-only
  runtime check, then disposable-lab crash or boundary test only when needed.
- Keep target-specific exploit chains, repro transcripts, and disclosure
  details in target folders or `references/`, not global memory.
