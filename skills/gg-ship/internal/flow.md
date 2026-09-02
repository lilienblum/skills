# Delivery flow

Run the work as a phase graph. Keep each role's objective and context distinct.

```text
EXPLORE -> PLAN -> WORK -> CRITIQUE -> PROMOTE
```

The phase graph may cycle. The executable plan inside `WORK` is a validated DAG when units have dependencies.

## Cycle budget

Use the finite review-cycle budget defined by `gg-ship`. Count every return from `CRITIQUE` to an earlier phase as one repair cycle.

## Internal phase skills

Load the current phase file, any selected route overlay, and only the dependencies they name; do not preload later phases. On transition, preserve the phase receipt and give the next phase only its named context plus the selected overlay.

- `explore.md` grounds facts, constraints, unknowns, and acceptance criteria.
- `plan.md` builds and validates the executable dependency graph.
- `work.md` executes ready nodes and records artifacts and receipts.
- `critique.md` independently judges the exact integrated revision.
- `promote.md` makes the accepted result visible on authorized destinations.

Use separate agents when available. Otherwise run distinct passes and do not let a phase judge its own output.

Follow the outcome rules in the current phase's `Transition` section. The main agent owns every transition and the integrated artifact. A phase cannot waive another phase's entry gate. Any changed artifact revision invalidates its critique receipt.
