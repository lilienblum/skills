# Fleet execution

Use for many independent units that benefit from a rolling worker pool. A long sequential task needs a checkpoint, not this machinery.

Keep a durable manifest of the goal, acceptance criteria, settled decisions, and each unit's dependencies, owner, state, retries, artifact identity, and checks. Include the integrated review verdict, consumed repair cycles, and remaining blockers. Use [execute-unit.md](execute-unit.md) for briefs and results.

Partition work into independently writable and verifiable units. Dispatch ready units within capacity, integrate results in dependency order, and refill the pool on completion. Leave enough budget for integration, review, and delivery; preserve resumable state when stopping.

For repeated transformations, validate a representative pilot before scaling out. Choose a capable worker within host policy; use cheaper tiers for matching units only when the pilot demonstrates they can do the work. A pilot is not required for unrelated tasks merely because they run in parallel.

The integrated result still needs `gg-review`. Add unit-level review before integration only when a specific risk would be costly or unsafe to defer. Reuse applicable evidence rather than repeating the same full review at both levels.

Report verified totals and material failed, abandoned, or blocked exceptions, not a worker-by-worker narrative.
