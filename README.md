# agents

What I use with agents.

## gg

How I ship bigger work: omp's native Goal keeps the session running; gg-ship adds the execution and independent-review rules.

- `/goal Use gg-ship to <goal>` — native persistent workflow; `/goal` must be first
- `/gg-review` — second look at a named change
- `gg-guardrails` — keep it simple and prove it
- `gg-reviewer` — the second-look agent (uses my slow model)

## Use it in omp

From GitHub:

```sh
omp plugin marketplace add lilienblum/agents
omp plugin install gg@agents
```

From this folder:

```sh
omp plugin marketplace add .
omp plugin install gg@agents
```

or:

```sh
omp plugin link ./plugins/gg
```

Then `/reload-plugins` or restart.
