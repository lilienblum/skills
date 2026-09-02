# Fleet route

Add this overlay to `flow.md` for dozens to hundreds of work units, long-running work, or a worker fleet coordinated by one main agent.

## Control plane

The main agent keeps the full task and a compact durable manifest:

```text
original goal and scope
acceptance criteria
settled decisions and user gates
current phase and transition reason
unit ID, dependencies, owner, state, and retry count
artifact locator and immutable revision
review mode, reviewer identifier when available, and review and verification verdicts for that revision
```

Workers receive only their unit brief. They do not receive the conversation or communicate with siblings.

## Plan additions

Partition the work into independently writable and verifiable nodes. Eliminate shared writes before adding coordination. Apply the `gg-write` agent-brief contract to every node.

## Work additions

After the representative pilot in `work.md` passes, route matching nodes to the cheapest capable tier with the smallest useful context:

- Cheap for search, extraction, inventory, classification, formatting, and known checks.
- Worker for bounded implementation, migrations, debugging, and test construction.
- Judgment for architecture, ambiguous tradeoffs, decomposition, and synthesis.
- Verifier for fresh-context review and behavioral proof.

Dispatch ready nodes through a rolling window and refill capacity on completion. Stop spawning near the execution budget and keep the manifest resumable. A cheaper tier escalates only after a capability failure, not a transient infrastructure failure. Never hard-code provider or model names.

## Critique and promotion additions

Run `gg-review` on consequential nodes as well as the integrated result. Use `gg-write` for large-run delivery.
