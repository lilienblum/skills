---
name: gg-handoff
description: "Pass compacted goals and context between agents"
argument-hint: "[id]"
license: MIT
---

# GG Handoff

Pack the current goal and only the context another agent needs to continue. Unpack a named handoff and continue immediately.

## Locate

`HANDOFF_DIR` is `<OS temp>/gg-handoff`. Resolve the OS temp dir with Python `tempfile.gettempdir()`, else `$TMPDIR` / `%TEMP%`, else `/tmp`. Create `HANDOFF_DIR` if missing. Each handoff is `HANDOFF_DIR/<id>.md`.

## Dispatch

- `$ARGUMENTS` starts with a positive integer token → **load** that id.
- Otherwise → **write**. Remaining arguments are the next session's focus.

## Write

Mint the smallest unused positive integer id in `HANDOFF_DIR`. Do not overwrite.

Write a short markdown file. Omit empty sections. Point at existing artifacts; do not paste them. Quote only when the exact wording is the contract. Redact secrets, tokens, passwords, and PII. Preserve exact paths, SHAs, branches, PR/ticket ids, and commands.

```markdown
# <id>

cwd: <absolute workspace>
branch: <git branch or none>
head: <short SHA or none>

## Goal
<durable outcome and observable acceptance>

## Remaining
<ordered next work>

## Done
<finished work the next agent must not redo>

## Decisions
<binding choices that would otherwise be re-litigated>

## Pointers
<paths, PRs, tickets, commands>

## Constraints
<blockers, budgets, do-not-touch>

## Skills
<skill names to load before continuing>
```

If a persistent Goal already exists, record its identity and status; do not duplicate its body.

After the file is written, the entire reply to the user is exactly:

```
Prompt in your agent:
/gg-handoff <id>
```

## Load

Read `HANDOFF_DIR/<id>.md`. If it is missing, say so with the expected path and stop.

Load the named skills. Adopt the goal, remaining work, decisions, constraints, and identifiers. Treat decisions as binding unless current evidence contradicts them. Work in the recorded `cwd` when that directory still exists; otherwise say so and stop.

Continue the remaining work immediately. Do not reprint the handoff. Do not re-ask settled questions.
