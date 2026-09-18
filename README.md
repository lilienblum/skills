# agents

Personal [oh-my-pi](https://github.com/oh-my-pi) marketplace: skills, plugins, agents.

## Install

```sh
omp plugin marketplace add lilienblum/agents
omp plugin install gg@agents
```

Local checkout, from this repo:

```sh
omp plugin marketplace add .
omp plugin install gg@agents
```

or link the plugin directly:

```sh
omp plugin link ./plugins/gg
```

Then `/reload-plugins` (or restart) so skills, commands, and agents load.

## gg

Ship substantial work under a Goal with independent review.

| Surface | What |
| --- | --- |
| `/gg-ship` | Own qualifying work through `/goal`, todo, task batch, and a blocking `gg-reviewer` `PASS` |
| `/gg-review` | Independent review via `gg-reviewer` (`@slow`) |
| `gg-guardrails` | Shared criteria; not a separate gate |
| `gg-reviewer` | Read-only agent, `@slow`, strict verdict schema |

Roles (`@plan`, `@task`, `@slow`, `@smol`, `@default`) come from your omp config. This plugin does not pin model ids.

Handoff is omp `/handoff`. Advisor is not the review gate. Vibe is not the ship path.

## Add more

Drop another plugin under `plugins/<name>/` (`skills/`, `agents/`, `commands/`, optional `package.json` with `"omp": {}`) and list it in `.omp-plugin/marketplace.json`.
