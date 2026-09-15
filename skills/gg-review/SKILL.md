---
name: gg-review
description: "Review a named change or design"
license: MIT
---

# GG Review

Review the named artifact against its intended behavior. Stay read-only unless the user requests edits or published comments.

## Establish the target

Identify the artifact and immutable revision or digest, acceptance source, relevant repository rules, and comparison base. If the target or intent cannot be established, return `INCONCLUSIVE`.

## Review

One reviewer covers the following concerns in a single pass. Add a specialist only when a concrete risk or independently reviewable area warrants it; do not create one worker per concern.

- **Correctness:** trace reachable behavior, invariants, failure modes, security boundaries, and evidence.
- **Fidelity:** compare requirements with behavior, including omissions and unrequested scope.
- **Standards:** apply documented conventions without duplicating deterministic checks.
- **Simplicity:** identify removable machinery, existing owners, and unjustified continuing cost.

Use `gg-guardrails` as shared criteria during this pass, not as another review or separate verdict. Verify material claims against the source and direct evidence. A reachable failure or concrete cost is required for a finding. Exclude unrelated pre-existing issues, taste, and unsupported speculation; merge duplicates and rank by impact.

After repairs, assess the new delta and affected behavior. Reuse earlier findings and evidence only after checking that the relevant code, dependencies, configuration, and environment remain applicable. Expand checks when impact is uncertain. Record a verdict for the current revision; never relabel an old verdict as current.

## Feedback

Return `PASS` when no blocker or material evidence gap remains, `NEEDS_CHANGES` for confirmed blockers, or `INCONCLUSIVE` when missing evidence prevents judgment. Report confirmed findings even when other material claims remain inconclusive. A deferred finding must be safe without making the current result incorrect.

Lead with actionable findings ordered by consequence. Include location, trigger, observed failure or concrete cost, evidence, and the smallest corrective direction. Preserve exact commands and identifiers. Record the reviewed artifact, revision, and verdict; disclose self-review when the reviewer also implemented the change. Do not claim independence from a separate pass in the same conversation.

If no material finding exists, say so plainly and name the review scope and checks. Omit empty sections, routine praise, diff narration, and worker bookkeeping.
