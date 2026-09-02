---
name: gg-guardrails
description: "Pressure-test a consequential change for needless complexity, hidden risk, and flimsy evidence."
license: MIT
---

# GG Guardrails

*Reject unjustified complexity, risk, and weak evidence.*

Apply these guardrails while planning, executing, reviewing, or accepting a consequential change. Judge the proposed system change, not merely the edited lines or an agent's account of them.

## Bind the target

During planning, bind the requested behavior, comparison point, and exact proposal. During execution, review, or acceptance, also bind the artifact locator and immutable revision or digest. A branch, tag, URL, or version label is a locator, not proof of identity.

Separate problems introduced or exposed by the change from unrelated pre-existing behavior. A pre-existing problem matters only when the change makes it reachable, worsens it, or makes it relevant to acceptance.

## Make every part earn its place

Try the smallest robust option in order:

1. Do nothing because the outcome already exists or is unnecessary.
2. Delete obsolete behavior or configuration causing the problem.
3. Reuse an existing owner, path, type, component, or convention.
4. Use a standard or platform capability already available.
5. Add a narrow local change.
6. Add a dependency only when it removes more complexity and risk than it adds.
7. Add an abstraction only when current requirements need it in multiple concrete places.

Inventory meaningful additions: components, services, dependencies, abstractions, generated layers, state transitions, configuration, permissions, queues, runtime branches, and operational steps.

For each addition, determine:

- which current requirement needs it;
- whether an existing owner can absorb it;
- whether it creates another source of truth or lifecycle;
- which concrete property justifies its continuing cost;
- which limitation the simpler design would accept.

Keep complexity when it provides a real security boundary, failure isolation, independent scaling, compatibility, auditability, or deployment constraint. Preserve validation, accessibility, observability, and data-loss protection.

## Trace the changed path

Follow the reachable behavior end to end where relevant:

- entry point, caller identity, and authorization;
- source of truth, state transitions, locks, and transactions;
- side effects and partial-failure points;
- error translation and user-visible symptoms;
- retries, limits, cleanup, recovery, and idempotency;
- provider, account, deployment, and local-development variants.

Probe concurrency around caps, uniqueness, leases, reservations, locks, and read-before-write decisions.

## Expand sensitive boundaries

For authentication, credentials, secrets, permissions, privileged operations, or tenant boundaries, verify principals, token purpose, reachable operations, scope checks, fallbacks, impersonation, empty-token paths, and why narrower permissions are insufficient.

Confirm external semantics from current authoritative documentation when the conclusion depends on them.

Treat APIs, SDKs, examples, names, errors, UI text, compatibility, migrations, rollout order, and generated artifacts as contracts.

## Require credible evidence

Prefer evidence that exercises the changed behavior: generated artifacts, provider or database integration, processes, networks, browsers, concurrency, or end-to-end flows.

Green checks prove only the paths they exercise. Compilation, snapshots, and object-construction tests are not substitutes for active-path evidence. Missing automation blocks only when a material correctness, security, compatibility, or operational claim cannot otherwise be established.

Work against the exact current target. Reject stale receipts, cached substitutes, and worker self-reports. A new artifact revision invalidates prior evidence.

## Result

Return the parts to remove or retain, the changed paths and boundaries checked, the evidence for each material claim, and one status:

- `PASS`: the current target satisfies the material guardrails.
- `FAIL`: a concrete guardrail violation remains.
- `INCONCLUSIVE`: missing identity, access, environment, or evidence prevents judgment.

`INCONCLUSIVE` never satisfies a completion gate.
