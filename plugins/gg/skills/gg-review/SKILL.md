---
name: gg-review
description: "Independent review of a named diff, branch, PR, or design. Challenge the artifact, verify evidence, return PASS, NEEDS_CHANGES, or INCONCLUSIVE."
license: MIT
---

# GG Review

Review the named artifact against its intended behavior. Stay read-only unless the user requests edits or published comments.

## Dispatch

If this session is already agent `gg-reviewer`, perform the review below.

Otherwise spawn one blocking `gg-reviewer` and wait for its structured verdict. Brief:

- goal and acceptance source
- governing rules
- comparison base
- exact artifact identity (path + revision or digest)
- diff and evidence pointers

Do not steer the verdict with implementer conclusions. Do not self-review in the same conversation and call it independent.

If `gg-reviewer` cannot spawn, one separate self-review pass against the source and checks; disclose self-review. Advisor notes are not a substitute.

Add `security-reviewer` only when a concrete independently reviewable security risk warrants it.

## Establish the target

Identify the artifact and immutable revision or digest, acceptance source, relevant repository rules, and comparison base. If the target or intent cannot be established, return `INCONCLUSIVE`.

## Review

One reviewer covers the following concerns in a single pass. Do not create one worker per concern.

- **Correctness:** trace reachable behavior, invariants, failure modes, security boundaries, and evidence.
- **Fidelity:** compare requirements with behavior, including omissions and unrequested scope.
- **Standards:** apply documented conventions without duplicating deterministic checks.
- **Simplicity:** identify removable machinery, existing owners, and unjustified continuing cost.

Use `gg-guardrails` as shared criteria during this pass, not as another review or separate verdict. Verify material claims against the source and direct evidence. A reachable failure or concrete cost is required for a finding. Exclude unrelated pre-existing issues, taste, and unsupported speculation; merge duplicates and rank by impact.

After repairs, assess the new delta and affected behavior. Reuse earlier findings and evidence only after checking that the relevant code, dependencies, configuration, and environment remain applicable. Expand checks when impact is uncertain. Record a verdict for the current revision; never relabel an old verdict as current.

## Feedback

Return `PASS` when no blocker or material evidence gap remains, `NEEDS_CHANGES` for confirmed blockers, or `INCONCLUSIVE` when missing evidence prevents judgment. Report confirmed findings even when other material claims remain inconclusive. A deferred finding must be safe without making the current result incorrect.

Lead with actionable findings ordered by consequence. Include location, trigger, observed failure or concrete cost, evidence, and the smallest corrective direction. Preserve exact commands and identifiers. Record the reviewed artifact, revision, and verdict.

If no material finding exists, say so plainly and name the review scope and checks. Omit empty sections, routine praise, diff narration, and worker bookkeeping.
