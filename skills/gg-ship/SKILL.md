---
name: gg-ship
description: "Ship substantial or high-risk build and ops tasks through planning, execution, review, and verified completion. Use for coordinated changes, migrations, and long-running delivery; exclude light, low-risk tasks."
license: MIT
---

# GG Ship

Own substantial implementation or operational work from the assigned goal through verified delivery.

## Scope

Use when work needs coordinated changes across components, dependent workstreams, sustained execution, or review because failure has significant consequences. A high-risk change can qualify even when the edit is small. Multiple steps alone do not justify this workflow.

Light, low-risk tasks are outside this skill. If invoked for a bounded low-risk fix or routine edit, execute directly with an appropriate check without loading this workflow or requiring its review gate.

## Workflow

Read [internal/flow.md](internal/flow.md). The main agent owns the goal, plan, integration, and delivery. Delegate only when independent work can usefully run in parallel or a concrete risk needs specialist attention. Use one independent final reviewer when the host supports it; otherwise perform a separate self-review and disclose that limitation.

Load [internal/execute-unit.md](internal/execute-unit.md) only for delegated work. Add [internal/fleet.md](internal/fleet.md) for many independently executable units requiring a rolling worker pool. Duration alone does not require a fleet.

## Recovery and user gates

Investigate recoverable failures and continue within scope without asking whether to retry. Inspect current state before retrying a mutation; repeat it only when safe against duplicate effects. A transient failure may justify the same attempt; a deterministic failure needs a changed approach.

Keep recovery finite. Default to two retries per failed operation and two repair cycles after review, unless the task sets other finite limits. At a limit, report the unresolved failure, attempts, and evidence; do not restart the budget through another worker or renamed step. Complete unaffected work where possible.

Follow host approval mechanisms. Ask the user only for unavailable authority, a dangerous or irreversible action requiring approval, a scope change, contradictory requirements, or a consequential choice without a defensible default. Authorization persists across recovery attempts but does not expand the assigned scope or destinations.

## Completion

Before reporting completion, reconcile the result with the original request and subsequent amendments. Account for every required outcome, including anything blocked or unfinished.

Done requires evidence for every acceptance criterion against the delivered artifact, a current `gg-review` `PASS`, and completion of all authorized delivery steps. Disclose self-review when no independent reviewer was available. Unresolved blockers or material evidence gaps prevent completion; record why any deferred finding is safe.

Report the outcome, strongest proof or artifact link, meaningful deviations or risks, and any required user action. Preserve exact identifiers and commands. Keep worker bookkeeping out of the final response.
