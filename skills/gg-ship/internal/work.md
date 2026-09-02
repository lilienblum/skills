# Work

Execute the validated plan and externalize current artifacts and receipts. Workers do not plan the task or accept their own output.

## Context

Receive the validated graph, ready nodes, integration state, acceptance criteria, and execution budget. Each delegated worker receives only one ready node with bounded context, write scope, checks, retry budget, and output contract; it does not receive unrelated conversation or sibling reasoning.

## Procedure

1. Execute ready nodes in dependency order and parallelize independent nodes within capacity.
2. Run a representative pilot before broad fan-out. Among representative candidates, prefer the highest-risk one.
3. Authorize cheaper workers only for units matching a demonstrated pilot pattern. A non-representative success does not authorize fan-out.
4. Record artifacts and receipts immediately and integrate in dependency order.
5. Classify failures before retrying or changing phases.

Use `execute-unit.md` for delegated nodes.

## Transition

- Stay in `WORK` for a transient local failure and retry with a materially changed attempt.
- Return to `PLAN` for a failed assumption, missing dependency, ownership conflict, or poor decomposition.
- Return to `EXPLORE` when new evidence changes the intended outcome or constraints.
- Enter `CRITIQUE` only with an integrated artifact, exact identity, and direct evidence for every acceptance criterion.
