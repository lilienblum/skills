---
name: gg-review
description: "Review a named diff, branch, PR, change request, or design. Challenge the artifact, verify the evidence, and call blockers plainly."
license: MIT
---

# GG Review

*Challenge consequential work before it is accepted.*

Challenge a diff, branch, change request, file set, or design. Report evidence-based findings. Keep the review read-only unless the user explicitly requests edits or published comments.

## Scope

Record:

- the exact artifact and immutable revision or digest;
- the intended behavior and acceptance source;
- relevant repository standards and surrounding context;
- the comparison base, when reviewing a change.

If the target or intent cannot be established, return `INCONCLUSIVE`.

## Shared guardrails

Apply `gg-guardrails` to establish the exact current artifact, comparison point, changed runtime path, sensitive boundaries, contracts, rollout, credible evidence, and whether every meaningful new part earns its cost.

Do not report a pre-existing problem unless the change makes it reachable, makes it worse, or makes it material to acceptance.

A `FAIL` guardrail result becomes a blocker. An `INCONCLUSIVE` result prevents `PASS` when it covers a material claim.

## Independent lenses

Run the lenses in isolated contexts. Parallelize when available; otherwise clear prior conclusions between passes.

1. **Correctness.** Trace behavior, invariants, edge cases, failure modes, security boundaries, and evidence.
2. **Fidelity.** Compare every requirement with the artifact. Find omissions, incorrect behavior, and unrequested scope.
3. **Standards.** Apply documented repository conventions. Do not duplicate checks already enforced deterministically.
4. **Simplicity.** Find removable machinery, existing owners, speculative flexibility, and unjustified operational cost.

Each lens cites exact evidence. A possibility without a reachable failure or concrete cost is not a finding.

## Lead judgment

After all lenses finish:

1. Verify findings against the artifact.
2. Merge duplicates across lenses.
3. Dismiss taste, unsupported speculation, and context errors.
4. Rank the remaining findings by impact.
5. Recommend the smallest corrective direction.

If a blocker makes the approach unusable, stop looking for low-impact nits. Still check for security defects, ownership violations, and portions that can be accepted independently.

## Record

Keep a compact record for the next agent or phase: verdict, locator, revision, and each finding's kind, confidence, lens, location, evidence, trigger, impact, and correction.

Verdict is `PASS`, `NEEDS_CHANGES`, or `INCONCLUSIVE`. Finding kind is `blocker`, `follow-up`, or `observation`. Confidence is `high`, `medium`, or `low`. Lens is `correctness`, `fidelity`, `standards`, or `simplicity`.

Use `NEEDS_CHANGES` for any blocker. A follow-up must be safe to defer without making the current artifact incorrect. An observation requires no action. Use `PASS` when no blocker remains. A changed revision requires a new review.

Apply `gg-write` to the final feedback.
