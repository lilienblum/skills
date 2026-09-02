# Critique

Judge the exact integrated artifact from fresh context. Do not receive worker rationale and do not fix by default.

## Context

Receive only the goal, acceptance criteria, artifact locator and immutable identity, changed behavior or diff, governing standards, and direct evidence.

## Procedure

1. Apply `gg-review` from fresh context; it owns the shared `gg-guardrails` pass.
2. Verify every material finding against the current artifact.
3. Classify each finding by its cause rather than sending every failure back to implementation.

## Receipt

Record the artifact revision, review mode (`separate-agent` or `isolated-pass`), reviewer or run identifier when available, verdict, and blocking finding IDs. Keep successful review metadata out of the final user response unless it is needed to establish trust; always surface unresolved findings.

## Transition

- Local implementation defect -> `WORK`.
- Stale or incomplete evidence -> `WORK`.
- Decomposition, ownership, or architecture defect -> `PLAN`.
- False premise, missing requirement, or misunderstood environment -> `EXPLORE`.
- No material finding and current evidence passes -> `PROMOTE`.

Any changed revision invalidates the prior critique. The new revision must return through `CRITIQUE` before promotion.
