---
name: gg-ship
description: "Ship substantial or high-risk changes under a persistent Goal through verified delivery"
license: MIT
---

# GG Ship

Own substantial implementation or operational work under a persistent Goal through verified delivery.

## Scope

Use when work needs coordinated changes across components, dependent workstreams, sustained execution, or review because failure has significant consequences. A high-risk change can qualify even when the edit is small. Multiple steps alone do not justify this workflow.

Light, low-risk tasks are outside this skill. If invoked for a bounded low-risk fix or routine edit, execute directly with an appropriate check without loading this workflow or requiring its review gate.

## Goal lifecycle

For qualifying work, inspect the current Goal before planning. Continue an unfinished Goal when it covers the assigned outcome; if none exists, invoke `/goal` with the requested outcome and observable acceptance criteria. Do not replace or repurpose an unrelated unfinished Goal; surface that conflict for user direction.

The Goal is the persistent completion contract; the plan is mutable execution state. Incorporate later in-scope instructions as amendments. Keep the Goal active while required work remains.

## Understand and plan

Inspect current behavior, repository rules, affected paths, and execution surfaces. Ground the outcome, constraints, and observable acceptance criteria. Resolve material unknowns from evidence, conventions, small experiments, or safe reversible defaults; do not carry assumptions forward as facts.

Use `gg-guardrails` to choose the smallest robust approach and identify relevant safety boundaries. Treat it as guidance, not a separate verdict or report. Write a short plan with the affected components, meaningful dependencies, and checks. Describe data shape, state transitions, compatibility, and failure behavior only where the change affects them.

An ordered list suffices for sequential work. When scheduling dependent workers, record unit IDs, dependencies, write ownership, and acceptance checks. Ensure dependencies exist, have no cycles, and release only ready units; concurrent workers must not share writes. Define a check for the integrated outcome without inventing an extra work unit for it.

## Execute

The main agent owns the plan, integration, and delivery. Delegate only when independent work can usefully run in parallel or a concrete risk needs specialist attention.

When delegating, give workers a self-contained brief rather than the full conversation. The main agent inspects their artifacts and integrates results; worker success reports are not acceptance evidence. For many independently executable units that need a rolling worker pool, use Fleet execution.

Run checks that exercise the changed behavior, including the integrated outcome. Preserve safety boundaries and fix root causes within scope. Update the plan when evidence changes dependencies or assumptions; investigate further when the Goal or environment was misunderstood.

For work spanning sessions, checkpoint only mutable execution state: decisions, artifact identities, remaining work and blockers, and consumed retry and repair counts. Do not duplicate the Goal.

### Delegated work

Skip unless delegating.

Give each worker a self-contained brief with:

- unit ID and bounded goal;
- allowed writes and relevant constraints;
- necessary facts and source pointers;
- acceptance criteria and direct checks;
- execution and retry budget;
- output location.

Missing information blocks only when it prevents safe execution. Return that blocker to the main agent rather than asking the user or inferring sibling state. Do not expand the assigned scope.

Inspect the affected path, make the smallest robust change, preserve relevant safety boundaries, and run the required checks. Fix root causes within the assigned scope; return a blocker if the necessary fix crosses it.

Leave the artifact at the agreed location. Return the unit ID, status (`ready`, `failed`, or `blocked`), artifact locator and revision or digest, changed paths, check commands and results, retries used, and material deviations or blockers. Include evidence pointers rather than unsupported success claims.

`ready` means the artifact exists and required local checks pass. It does not mean independently reviewed or accepted. A failed required check means `failed`; missing authority, unsafe ambiguity, or an impossible requirement means `blocked`.

### Fleet execution

Skip unless a rolling worker pool is required. Duration alone does not require a fleet. A long sequential task needs only the Goal and a compact checkpoint, not this machinery.

Keep a durable execution manifest tied to the Goal, with settled decisions and each unit's dependencies, owner, state, retries, artifact identity, and checks. Include the integrated review verdict, consumed repair cycles, and remaining blockers; do not duplicate the Goal's outcome or status. Brief and collect results as in Delegated work.

Partition work into independently writable and verifiable units. Dispatch ready units within capacity, integrate results in dependency order, and refill the pool on completion. Leave enough budget for integration, review, and delivery; preserve resumable state when stopping.

For repeated transformations, validate a representative pilot before scaling out. Choose a capable worker within host policy; use cheaper tiers for matching units only when the pilot demonstrates they can do the work. A pilot is not required for unrelated tasks merely because they run in parallel.

The integrated result still needs `gg-review`. Add unit-level review before integration only when a specific risk would be costly or unsafe to defer. Reuse applicable evidence rather than repeating the same full review at both levels.

Report verified totals and material failed, abandoned, or blocked exceptions, not a worker-by-worker narrative.

## Review and repair

Use `gg-review` once on the integrated result, with one independent reviewer when available. Give the reviewer the goal, acceptance source, governing rules, comparison base, exact artifact identity, diff, and direct evidence. Supply necessary factual context without steering the verdict with worker conclusions.

If only self-review is possible, perform a separate pass against the source and checks; record it as self-review, not isolated or independent review. Record the verdict, reviewed revision, mode, and unresolved findings.

Fix confirmed blockers and missing evidence within the repair budget. A repair requires a current verdict: review the delta and affected behavior, retaining earlier findings and checks only when their continued applicability is established. Expand review when shared dependencies, assumptions, or boundaries changed. Never transfer an old `PASS` to a new revision without this assessment.

## Deliver

Complete the destinations already authorized by the task, such as a local artifact, PR, or deployment. Do not invent publication or notification requirements. Verify external writes when the destination permits readback and verify deployed behavior when relevant to acceptance.

If delivery exposes a defect or changes the artifact, repair and obtain an updated review before completing the Goal.

## Recovery and user gates

Investigate recoverable failures and continue within scope without asking whether to retry. Inspect current state before retrying a mutation; repeat it only when safe against duplicate effects. A transient failure may justify the same attempt; a deterministic failure needs a changed approach.

Keep recovery finite. Default to two retries per failed operation and two repair cycles after review, unless the task sets other finite limits. At a limit, report the unresolved failure, attempts, and evidence; do not restart the budget through Goal continuation, another worker, or a renamed step. Complete unaffected work where possible. A retry limit alone does not justify marking the Goal blocked; follow the Goal's blocking rule.

Follow host approval mechanisms. Ask the user only for unavailable authority, a dangerous or irreversible action requiring approval, a scope change, contradictory requirements, or a consequential choice without a defensible default. Authorization persists across recovery attempts but does not expand the assigned scope or destinations.

## Completion

Before completing the Goal, reconcile the delivered result with it and subsequent amendments. Account for every required outcome, including anything blocked or unfinished.

Complete the Goal only after every acceptance criterion has evidence against the delivered artifact, the delivered revision has a current `gg-review` `PASS`, and all authorized delivery steps are complete and verified. Disclose self-review when no independent reviewer was available. Unresolved blockers or material evidence gaps prevent completion; record why any deferred finding is safe.

Report the outcome, strongest proof or artifact link, meaningful deviations or risks, and any required user action. Preserve exact identifiers and commands. Keep worker bookkeeping out of the final response.
