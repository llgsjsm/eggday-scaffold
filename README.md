# Eggday Vulnerability Research Scaffold

I vibe coded this README.md :P

A lightweight, agent-friendly scaffold for responsible vulnerability research:
start from a small threat model, audit one thin slice, verify with safe
evidence, check novelty, then report or park.

The goal is to avoid turning the workspace itself into a haystack. Keep active
context small and pull deep notes only when the current target needs them.

This repository is the scaffold only: docs, folder skeleton, and templates. It
ships with no targets, findings, exploits, or artifacts.

## Start Here

1. Copy or clone this tree into a new workspace directory.
2. Read `MEMORY.md` and `METHODOLOGY.md` once, and keep them in active context.
3. Open a target:

   ```sh
   mkdir -p targets/<slug>/{analysis,findings,pocs,artifacts}
   cp THREAT_MODEL_TEMPLATE.md targets/<slug>/THREAT_MODEL.md
   ```

4. Fill the threat card before asking for bugs, then pick one thin slice.
5. Keep `targets/<slug>/README.md` current enough that the next session can
   resume from the strongest lead.

`AGENTS.md` holds agent-facing operating policy and is picked up automatically
by Claude Code and other AGENTS.md-aware tools.

## Default Context

When starting or resuming work, read in this order:

1. `README.md` for workspace layout.
2. `MEMORY.md` for persistent operating rules.
3. `METHODOLOGY.md` for the active audit loop.
4. The target folder's `README.md` or `THREAT_MODEL.md`.
5. One focused candidate, finding, or verifier note.

Do not preload long repro logs, disclosure drafts, old case studies, extracted
source trees, package dumps, or unrelated target notes unless the current slice
depends on them.

## Core Files

- `MEMORY.md`: compact workspace memory and safety posture.
- `METHODOLOGY.md`: one-page default vulnerability research loop.
- `THREAT_MODEL_TEMPLATE.md`: template for new target threat cards.
- `references/detailed-vulnerability-research-methodology.md`: longer
  methodology and case-study reference.

## Folder Layout

- `targets/`: active target folders, one target per slug.
- `incoming/`: temporary landing area for unsorted notes, packages, logs, or
  external material.
- `_shared/`: shared source checkouts, advisory corpora, symbols, SDKs, and
  other reusable corpora.
- `_archive/`: parked or stale target material that should not load by default.
- `references/`: stable methodology notes, background references, and reusable
  writeup guidance.

## Target Folder Shape

Each active target should prefer this structure:

- `README.md`: short target status, environment facts, strongest leads, and
  next action.
- `THREAT_MODEL.md`: attacker model, crown jewels, entry points, trust
  boundaries, invariants, verifier plan, and novelty gate.
- `analysis/`: source traces, experiments, notes, scratch repro scripts, and a
  `known-fixes.md` when patch lineage is part of the audit.
- `findings/`: evidence-backed candidates, reports, disclosure drafts, and
  final writeups.
- `pocs/` or `tools/`: marker-only repros, harnesses, probes, and helpers.
- `artifacts/`: binaries, extracted packages, logs, captures, and generated
  evidence. Avoid loading this by default.

## Research Discipline

For each target, state the attacker model before asking for bugs. Good prompts
and notes should name:

- attacker capability and prerequisite;
- reachable entry point;
- trust boundary;
- invariant that should hold;
- sensitive sink or consequence;
- verifier that would prove or disprove the hypothesis.

Prefer concrete questions such as "how can this low-privileged API user violate
the page-rendering secret boundary?" over broad requests such as "find all
vulnerabilities."

## Variant and Novelty Discipline

Treat a known vulnerability or patch as both a collision source and a discovery
seed. Once its broken invariant is understood, run three explicit passes:

- sibling vulnerabilities across adjacent or equivalent surfaces;
- incomplete fixes across omitted paths, callers, states, widths, or versions;
- fix bypasses and regressions across transformations, check/use boundaries,
  configuration changes, and later refactors.

The novelty gate must then compare current and historical advisories, public
issues, release notes, commits, patches, subsystem identifiers, bug-class
terms, and vulnerable and fixed code expressions. Compare root cause,
reachability, boundary, primitive, affected versions, and expected fix. The
absence of an advisory title match is not proof of novelty, and relationship to
a known CVE does not automatically make a reachable independent variant a
duplicate.

## Evidence and Safety

Research should produce source locations, reachability, root cause, verifier
output, fix guidance, variant-analysis results, novelty notes, and
disclosure-ready caveats.

Runtime validation should climb the ladder:

1. Static proof and exact references.
2. Local model or unit/integration test.
3. Instrumented harness or marker-only probe.
4. Disposable VM boundary/crash test if safer checks are insufficient.

Avoid destructive tests against production systems, unrelated files, valuable
devices, or real user data. Keep payload chains, long repro transcripts, and
target-specific operational details inside the relevant target folder rather
than global workspace docs.

## Maintenance Rules

- Keep this README as a map, not a case-study dump.
- Keep `MEMORY.md` compact and target-neutral.
- Keep target `README.md` files current enough that the next session can resume
  from the strongest lead.
- Fix broken note links as soon as they appear.
- Move stale or bulky material into `references/`, `findings/`, `artifacts/`,
  or `_archive/` instead of loading it into the default audit context.

## License

MIT. See `LICENSE`.
