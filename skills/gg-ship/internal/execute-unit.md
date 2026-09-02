# Execute unit

Complete exactly one bounded unit. Return an artifact and a structured receipt, not a conversation.

## Brief gate

The brief must provide `ID`, `GOAL`, `SCOPE`, `CONTEXT`, `ACCEPTANCE`, `VERIFY`, `TIMEBOX`, and `OUTPUT`.

If a missing field prevents safe execution, return `blocked`. Do not ask the user, contact sibling workers, infer sibling state, or expand the unit.

## Procedure

1. Read the brief as the complete source of intent.
2. Inspect only the context needed to understand the affected path.
3. Apply `gg-guardrails` to the unit and use its smallest viable option.
4. Execute only inside the allowed write scope.
5. Run the specified checks against the produced artifact.
6. Retry only transient or recoverable failures with a meaningfully different attempt. Default maximum: two retries.
7. Externalize the artifact at the required location.
8. Return the receipt and stop.

## Rules

- Fix the root cause inside the unit when evidence identifies it. Do not patch only the named symptom.
- Do not rewrite unrelated code or improve adjacent areas.
- Do not claim independent verification. Local checks make the artifact ready for verification.
- Do not fabricate outputs, identifiers, checks, or success.
- A failed required check produces `failed`, not `ready`.
- Missing access, unsafe ambiguity, or an impossible acceptance criterion produces `blocked`.

## Receipt

```yaml
status: ready | failed | blocked
unit_id: <brief identifier>
artifact:
  locator: <branch, commit, path, URL, or object ID>
  revision: <exact hash or version when available>
changed:
  - <path or object>
checks:
  - command: <exact command or procedure>
    result: pass | fail | not-run
    evidence: <output or artifact pointer>
retries: <count>
deviations:
  - <acceptance deviation, or none>
blocker: <specific blocker and exhausted alternatives, or none>
```

`ready` requires an externalized artifact and passing required local checks. The caller decides whether the artifact is accepted.
