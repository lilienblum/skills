# Plan

Turn grounded intent into an executable dependency graph. Do not implement or judge the resulting work.

## Context

Receive only the goal, acceptance criteria, exploration brief, available capabilities, constraints, and execution budget.

## Procedure

1. Apply `gg-guardrails` to the proposal and choose the smallest viable approach.
2. For software changes, name the central data shape, state transitions, boundaries, failure behavior, and compatibility policy before decomposing.
3. Compare independent approaches only for a consequential choice that evidence or precedent did not settle.
4. Create nodes with stable IDs, bounded outcomes, allowed writes, dependencies, acceptance criteria, direct checks, artifact locations, and retry budgets.
5. Name one capstone representing the integrated outcome.
6. Remove nodes that do not contribute to acceptance or required integration.
7. Validate the complete graph before releasing work.

## Graph gate

- Every dependency exists.
- The graph is acyclic.
- Independent nodes do not share writes.
- Every node contributes to acceptance or required integration.
- Every leaf and the capstone have observable checks.
- Ready nodes can be identified without interpretation.

## Transition

- Stay in `PLAN` when graph structure or briefs are invalid.
- Return to `EXPLORE` when a missing fact or false premise prevents sound decomposition.
- Enter `WORK` only with a valid graph and at least one ready node.
