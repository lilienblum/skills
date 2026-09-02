---
name: gg-ship
description: "Ship a build or ops task end to end: plan it, do it, review it, fix it, prove it."
license: MIT
---

# GG Ship

*Own assigned work through verified completion.*

Take a human-assigned implementation or operational task from request to verified result. The human defines the goal and scope; the agent owns the execution path.

## Contract

- Preserve the requested outcome and scope.
- Resolve reversible ambiguity from evidence, experiments, conventions, or a safe default.
- Keep workers independent. They receive bounded briefs, not the conversation.
- Trust artifacts and checks, not worker summaries.
- Do not require user attention for routine progress or recoverable failures. Follow host-required status and approval mechanisms without turning them into conversational gates.

## Procedure

1. Frame the goal, boundaries, artifact, and acceptance criteria from the task and environment.
2. Match one execution path and read it before planning:
   - Dozens to hundreds of units, long-running work, or a worker fleet: `internal/flow.md` plus `internal/fleet.md`.
   - Other multi-step work (phased path): `internal/flow.md`.
   - Small bounded task with material effects: inspect and plan inline, apply `gg-guardrails` to the plan, execute directly, review the exact result with `gg-review` from an isolated context, repair within the review-cycle budget, then promote with `gg-write`.
   - Trivial task: execute directly, run the direct check, apply `gg-guardrails`, then promote with `gg-write`. A task is trivial only when it is a localized mechanical edit, such as a typo, formatting, or comment change, with no runtime, data, security, permission, dependency, compatibility, or operational effect. When classification is uncertain, use the reviewed small-task path.
3. Load only the public skills and internal files named by the selected path.
4. Follow outcome-based transitions through a current artifact and independent proof. Repair failed gates without involving the user when a safe route remains.
5. Apply `gg-write` where named. Deliver the final user result only after the completion gate passes or a genuine user gate blocks all useful work.

Automatic review -> repair -> review cycling is finite. Default to at most two repair cycles per task unless the user or execution budget sets another finite limit. At the limit, stop cycling and return a concise blocker with the unresolved finding and current evidence.

## Recover without escalation

A failed command, deployment, check, worker, safety precondition, stale job, queue entry, conflict, or transient provider error is not a user gate. It is evidence to investigate.

When execution fails:

1. Inspect the exact failure, current state, logs, diffs, and affected environment.
2. Preserve safety and the requested scope; do not blindly bypass a guard.
3. Repair the cause, isolate the requested change, cancel or supersede stale work, retry with a materially different attempt, or choose another compliant route.
4. Re-run the direct checks against the resulting artifact.
5. Continue until the outcome is verified or every reasonable in-scope route is exhausted.

The original task authorizes ordinary reversible actions needed to finish it in the named environment. Do not add a separate conversational confirmation for an in-scope action merely because the tool has its own approval mechanism; invoke the tool and let the platform enforce approval. Do not ask merely because an attempt failed, the next route is broader internally, or production-like systems feel consequential. Ask only when the action crosses the original scope, changes the named environment, is irreversible or dangerous, requires unavailable authority, or presents a genuine choice in user-visible behavior.

For a delivery task, do not stop after diagnosing a recoverable implementation failure, receiving a failed receipt, or identifying a proposed next step. A blocker report is valid only after bounded alternatives have actually been attempted and no useful work can continue.

## User gates

Interrupt the user only for:

- an irreversible or dangerous action;
- missing access or credentials;
- contradictory requirements;
- a genuine product choice with no defensible default;
- a terminal blocker after bounded alternatives fail.

Batch gates, include a recommendation and default, and route other work around them. Do not require user input while runnable work remains. Provide only host-required, concise, non-blocking progress. Never ask whether to continue, whether to retry, or whether to use an ordinary recovery path already inside the task's scope.

## Completion gate

Done means:

- every acceptance criterion has evidence against the current integrated artifact;
- every non-trivial delivery has a current `gg-review` `PASS` verdict for that exact artifact revision;
- every blocking review finding is resolved; a non-blocking finding may remain only with a documented reason it is safe to defer;
- every required verdict is current and conclusive;
- the final message contains only the outcome, proof, meaningful deviations, and required user actions.
