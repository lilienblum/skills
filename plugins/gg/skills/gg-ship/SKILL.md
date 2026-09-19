---
name: gg-ship
description: "Ship substantial or high-risk omp work under its native Goal mode through verified delivery."
license: MIT
---

# GG Ship

Own substantial implementation or operational work inside omp's native Goal mode through verified delivery.

OMP-only. Do not invent handoff files, fleets, or extra coordinators. Do not hardcode model ids.

## Scope

Use when work needs coordinated changes across components, dependent workstreams, sustained execution, or review because failure has significant consequences. A high-risk change can qualify even when the edit is small. Multiple steps alone do not justify this workflow.

Light, low-risk tasks are outside this skill. If invoked for a bounded low-risk fix or routine edit, execute directly with an appropriate check without loading this workflow or requiring its review gate.

## Goal

Use omp's native Goal mode. The user starts it with `/goal Use gg-ship to <outcome>`. `/goal` must be the first command in the prompt; never try to invoke it from skill text.

The native Goal is the persistent completion contract. `todo` is mutable execution state. Incorporate later in-scope instructions as amendments. Keep working while required outcomes remain.

## Understand and plan

Inspect current behavior, repository rules, affected paths, and execution surfaces. Ground the outcome, constraints, and observable acceptance criteria.

This session stays on whatever model is already selected. Do not try to switch it with `@plan` / `@task` / `@smol` in prose — that does nothing.

Unsettled architecture → spawn `scout` for read-only mapping, then plan here.

Apply `gg-guardrails` as guidance, not a separate verdict. Write a short plan with affected components, meaningful dependencies, and checks. Init `todo`. Describe data shape, state transitions, compatibility, and failure behavior only where the change affects them.

`/prewalk` is a user/session switch (plan here, `@smol` after first edit). Mention it; do not assume it is on.

## Execute

The main agent owns the plan, integration, and delivery on this session's model. Delegate only when independent work can usefully run in parallel. Different models happen by spawning agents (`scout`, `task`, `sonic`, `gg-reviewer`), not by tagging roles in chat.

One `task` batch per fan-out. Required `context` is shared background. Each item is a self-contained brief (files, constraints, acceptance, checks). Follow up with `hub send`; revive parked workers instead of respawning.

| Work | Agent |
| --- | --- |
| Read-only mapping | `scout` |
| Implementation slice | `task` (default) |
| Mechanical / high-volume similar units | `sonic` |

Eval `workpool()` only for many independently executable similar units. Pilot one unit on `task` before scaling onto `sonic`. Duration alone is not a fleet.

Do not use vibe mode. Do not use `orchestrate` or `workflowz` as the ship path.

Run checks that exercise the changed behavior, including the integrated outcome. Preserve safety boundaries and fix root causes within scope.

### Worker brief

Skip unless delegating.

- unit ID and bounded goal
- allowed writes and constraints
- necessary facts and source pointers
- acceptance criteria and direct checks
- retry budget
- output location (`local://` or `agent://`)

Missing information blocks only when it prevents safe execution. Return that blocker rather than asking the user or inferring sibling state.

`ready` means the artifact exists and required local checks pass — not independently reviewed. Failed required check → `failed`. Missing authority, unsafe ambiguity, or impossible requirement → `blocked`.

## Review

Once the integrated result exists, spawn blocking `gg-reviewer` with `schemaMode: "strict"`. Give goal, acceptance, rules, comparison base, exact artifact identity, diff, and evidence pointers. Do not steer the verdict.

`PASS` is required to complete. Repair confirmed blockers within two cycles, then re-review the new revision. Never transfer an old `PASS` to a new revision.

If `gg-reviewer` cannot spawn, one separate self-review pass; disclose it. Advisor/WATCHDOG is not the gate.

## Deliver

Complete destinations already authorized by the task. Do not invent publication requirements. Verify external writes when the destination permits readback.

If delivery exposes a defect or changes the artifact, repair and obtain an updated review before the Goal completes.

## Recovery and user gates

Investigate recoverable failures and continue within scope. Inspect current state before retrying a mutation. Transient failure may retry the same attempt; deterministic failure needs a changed approach.

Default: two retries per failed operation, two repair cycles after review. At a limit, report the unresolved failure, attempts, and evidence; do not restart the budget through another worker or renamed step.

Do not use `ask` for recoverable choices or confirmation. Select the safest conventional default and continue. Use `ask` only when unavailable authority or a dangerous irreversible action truly prevents safe progress.

## Session continuity

Stay in this session. Use `/handoff` when the live context must collapse into a durable document on this session. Use `hub` to revive parked workers. Do not write temp-file handoffs.

## Completion

Reconcile the delivered result with the Goal and later amendments. Account for every required outcome, including anything blocked or unfinished.

Do not complete the Goal until every acceptance criterion has evidence against the delivered artifact, the delivered revision has a current `gg-reviewer` `PASS`, and authorized delivery steps are complete. Disclose self-review when no independent reviewer ran. Unresolved blockers or material evidence gaps prevent completion.

Report the outcome, strongest proof, meaningful deviations or risks, and any required user action. Preserve exact identifiers and commands. Keep worker bookkeeping out of the final response.
