# Delegated work

## Brief

Give each worker a self-contained brief with:

- unit ID and bounded goal;
- allowed writes and relevant constraints;
- necessary facts and source pointers;
- acceptance criteria and direct checks;
- execution and retry budget;
- output location.

Missing information blocks only when it prevents safe execution. Return that blocker to the main agent rather than asking the user or inferring sibling state. Do not expand the assigned scope.

## Execution

Inspect the affected path, make the smallest robust change, preserve relevant safety boundaries, and run the required checks. Fix root causes within the assigned scope; return a blocker if the necessary fix crosses it.

Retry within the brief's budget, defaulting to two retries. Inspect state before retrying mutations and guard against duplicate effects. Repeating a safe attempt can resolve a transient failure; change the approach for a deterministic failure.

Leave the artifact at the agreed location. Return the unit ID, status (`ready`, `failed`, or `blocked`), artifact locator and revision or digest, changed paths, check commands and results, retries used, and material deviations or blockers. Include evidence pointers rather than unsupported success claims.

`ready` means the artifact exists and required local checks pass. It does not mean independently reviewed or accepted. A failed required check means `failed`; missing authority, unsafe ambiguity, or an impossible requirement means `blocked`.
