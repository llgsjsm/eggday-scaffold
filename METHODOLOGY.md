# Minimal Vulnerability Research Methodology

This is the default protocol for agentic vulnerability research in this
workspace. Keep it short in active context. Pull detailed case studies from
`references/` only when a current slice needs them.

## Operating Rule

Start every audit from a small threat model, then work one thin slice at a
time. A useful slice names an attacker, an entry point, a trust boundary, a
security invariant, and a verifier.

Avoid broad prompts such as "find all vulnerabilities." They produce noise.
Prefer prompts that ask how a specific invariant can be violated by a specific
attacker through a specific surface.

## Default Loop

1. Scope the target
   - product, version, commit, build, platform, and local lab state
   - responsible-use constraints and destructive-test boundaries

2. Build the threat card
   - attacker model and prerequisites
   - crown-jewel functionality or assets
   - entry points and trust boundaries
   - high-risk operations such as authz, parsing, deserialization, file writes,
     kernel object lifetime, native bindings, IPC, sandbox exits, or caching

3. Pick one slice
   - auth boundary, request parser, file upload, plugin boundary, ioctl,
     syscall-like path, updater, archive extraction, token validation, cache
     keying, object lifetime, or cross-tenant data flow

4. Reconstruct invariants
   - state the rule in plain language
   - identify guards, assumptions, and caller/callee contracts
   - mark which inputs or states are attacker-controlled

5. Trace evidence
   - exact files, functions, selectors, routes, IOCTLs, handlers, or callbacks
   - attacker input to sensitive sink
   - guard conditions and bypass conditions

6. Run variant analysis
   - sibling vulnerabilities in adjacent or equivalent surfaces
   - incomplete fixes that cover only part of the vulnerable state space
   - fix bypasses or regressions that invalidate, evade, or weaken a guard

7. Verify safely
   - static proof and line references first
   - local model, unit test, integration test, fuzzer, harness, or marker probe
   - disposable VM crash tests only after safer checks answer too little

8. Gate novelty
   - compare with current and historical advisories, CVEs/GHSAs, changelogs,
     public issues, upstream commits, and fixes
   - search subsystem and function names, bug-class terms, and vulnerable and
     fixed code expressions
   - distinguish an exact duplicate from a related but independently reachable
     variant before investing in a full report

9. Record and decide
   - proven, disproven, duplicate, blocked, or needs a narrower slice
   - next verifier or patch guidance

## Required Variant Analysis

Run these passes when a candidate has plausible attacker reachability or when
a known vulnerability or patch is being used as a discovery seed.

- Sibling pass: apply the same invariant to adjacent callers, API versions,
  compatibility layers, alternate selectors, mirrored parsers or serializers,
  platform variants, error paths, and legacy entry points.
- Incomplete-fix pass: check whether the fix covered every source, caller,
  sink, width, object state, configuration, and supported input form. Look for
  validation present only in one wrapper or only as a debug assertion.
- Bypass/regression pass: follow the value after validation through
  normalization, conversion, mutation, caching, and check/use boundaries.
  Check whether later refactoring reordered, weakened, or removed the guard.

For each pass, record the surfaces checked, evidence, negative results, and any
candidate promoted for verification. Mark a pass `not applicable` with a short
reason rather than silently omitting it.

## Novelty Gate Standard

The novelty gate is evidence-backed collision analysis, not a search for a
matching advisory title. Record the sources, queries, repositories, and search
date, then compare the candidate's attacker model, entry point, trust boundary,
root cause, security primitive, affected versions, and expected fix with known
issues.

Classify the relationship as one of: exact duplicate, sibling variant,
incomplete fix, fix bypass, regression, independent root cause, or unresolved.
A candidate related to an existing CVE may still be novel when it reaches an
unfixed path or version, crosses a different boundary, has an independent root
cause, or creates a materially different security primitive. No public match
means only that no collision was found in the sources checked.

## Evidence Standard

A candidate is not a finding until it has at least:

- affected code or binary offsets;
- reachability from the stated attacker model;
- root-cause invariant break;
- impact hypothesis with caveats;
- verifier output or a concrete reproduction plan;
- variant-analysis notes, including negative results;
- novelty notes and sources checked.

## Context Budget

Keep stable scaffolding small. Default active context should usually be:

- root `README.md`;
- `MEMORY.md`;
- this file;
- the current target's `THREAT_MODEL.md` or one-page `README.md`;
- one focused candidate or finding note.

Do not preload long repro logs, full disclosure drafts, broad checklist
libraries, or unrelated target notes. Spend the bulk of work on focused source
navigation and verifier loops.

## Target Folder Convention

Each active target should prefer:

- `README.md`: one-page status, target facts, strongest leads, and next action;
- `THREAT_MODEL.md`: attacker model, boundaries, invariants, and slice plan;
- `analysis/`: notes, traces, experiments, scripts, and a per-target
  `known-fixes.md` when patch lineage matters;
- `findings/`: evidence-backed candidate or disclosure writeups;
- `pocs/` or `tools/`: marker-only repros, harnesses, and helpers.

Use `THREAT_MODEL_TEMPLATE.md` when opening a new target.
