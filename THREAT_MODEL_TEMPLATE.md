# <Target> Threat Model

Copy this into `<target>/THREAT_MODEL.md` and keep it to about one page while
the audit is active. Link out to deeper notes instead of expanding this file.

## Status

- Target:
- Version, commit, or build:
- Lab state:
- Current decision: exploring / validating / reporting / parked

## Attacker Model

- Actor:
- Access level:
- Inputs controlled:
- Inputs not controlled:
- Required prerequisites:
- Explicitly out of scope:

## Crown Jewels

- Security-sensitive asset or behavior:
- Why compromise matters:
- Expected security boundary:

## Entry Points

- Public or low-privilege entry points:
- Internal but attacker-reachable transitions:
- Configuration-dependent surfaces:

## Trust Boundaries

- Boundary:
- Trusted side:
- Untrusted side:
- Guard that is supposed to enforce it:

## High-Risk Operations

- Parsing, decoding, or deserialization:
- Authn/authz/session/token logic:
- File, archive, update, plugin, or template handling:
- Native, kernel, IPC, sandbox, or privilege boundary:
- Caching, tenant isolation, or cross-user state:

## Invariants

- Invariant 1:
- Invariant 2:
- Invariant 3:

For each invariant, ask: what attacker-controlled input or state transition can
violate it, and where would the violation become observable?

## First Thin Slices

1. Slice:
   - Entry point:
   - Sensitive sink:
   - Invariant under test:
   - Expected verifier:

2. Slice:
   - Entry point:
   - Sensitive sink:
   - Invariant under test:
   - Expected verifier:

## Variant Analysis

- Seed advisory, issue, commit, patch, or invariant:
- Sibling pass: adjacent APIs, callers, versions, compatibility paths, mirrored
  implementations, alternate selectors, and error paths checked:
- Incomplete-fix pass: omitted sources, sinks, widths, states, configurations,
  or input forms checked:
- Bypass/regression pass: post-validation conversions, mutations, caching,
  check/use boundaries, and later refactors checked:
- Negative results and surfaces ruled out:
- Variants promoted for verification:

## Verifier Plan

- Static proof:
- Local model or unit test:
- Integration or harness:
- Disposable VM or crash-only step:
- Negative control:

## Novelty Gate

- Current advisories/CVEs/GHSAs checked:
- Historical advisories and release notes checked:
- Vendor/upstream issues, commits, changelogs, and patches checked:
- Subsystem/function names, bug-class terms, and old/fixed expressions searched:
- Search date and sources not yet covered:
- Candidate versus known issue: attacker, entry point, boundary, root cause,
  primitive, affected versions, and expected fix:
- Classification: exact duplicate / sibling variant / incomplete fix / fix
  bypass / regression / independent root cause / unresolved
- Novelty confidence and remaining collision risk:

An absent advisory match is not, by itself, evidence of novelty.

## Decision Log

- Date:
- Observation:
- Decision:
- Next action:
