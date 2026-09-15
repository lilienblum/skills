# Delivery workflow

## Understand and plan

Inspect current behavior, repository rules, affected paths, and execution surfaces. Ground the outcome, constraints, and observable acceptance criteria. Resolve material unknowns from evidence, conventions, small experiments, or safe reversible defaults; do not carry assumptions forward as facts.

Use `gg-guardrails` to choose the smallest robust approach and identify relevant safety boundaries. Treat it as guidance, not a separate verdict or report. Write a short plan with the affected components, meaningful dependencies, and checks. Describe data shape, state transitions, compatibility, and failure behavior only where the change affects them.

An ordered list suffices for sequential work. When scheduling dependent workers, record unit IDs, dependencies, write ownership, and acceptance checks. Ensure dependencies exist, have no cycles, and release only ready units; concurrent workers must not share writes. Define a check for the integrated outcome without inventing an extra work unit for it.

## Execute

Implement directly unless useful parallel work or a specialist need justifies delegation. Use [execute-unit.md](execute-unit.md) for worker briefs and results. Give workers the relevant intent, constraints, source pointers, and bounded write scope rather than the full conversation. The main agent inspects their artifacts and integrates results; worker success reports are not acceptance evidence.

Run checks that exercise the changed behavior, including the integrated outcome. Preserve safety boundaries and fix root causes within scope. Update the plan when evidence changes dependencies or assumptions; investigate further when the Goal or environment was misunderstood. Follow the recovery budget in `gg-ship`.

For work spanning sessions, checkpoint only mutable execution state: decisions, artifact identities, remaining work and blockers, and consumed retry and repair counts. Do not duplicate the Goal. This does not require a worker fleet.

## Review and repair

Use `gg-review` once on the integrated result, with one independent reviewer when available. Give the reviewer the goal, acceptance source, governing rules, comparison base, exact artifact identity, diff, and direct evidence. Supply necessary factual context without steering the verdict with worker conclusions.

If only self-review is possible, perform a separate pass against the source and checks; record it as self-review, not isolated or independent review. Record the verdict, reviewed revision, mode, and unresolved findings.

Fix confirmed blockers and missing evidence within the repair budget. A repair requires a current verdict: review the delta and affected behavior, retaining earlier findings and checks only when their continued applicability is established. Expand review when shared dependencies, assumptions, or boundaries changed. Never transfer an old `PASS` to a new revision without this assessment.

## Deliver

Complete the destinations already authorized by the task, such as a local artifact, PR, or deployment. Do not invent publication or notification requirements. Verify external writes when the destination permits readback and verify deployed behavior when relevant to acceptance.

If delivery exposes a defect or changes the artifact, repair and obtain an updated review before completing the Goal.
