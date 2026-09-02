---
name: gg-write
description: "Turn gg-ship and gg-review output into tight briefs, sharp findings, and no-drama completion receipts."
license: MIT
---

# GG Write

*Make delivery artifacts concise, exact, and actionable.*

Format the agent-facing and user-facing artifacts produced by `gg-ship` and `gg-review`. Do not apply this skill to ordinary technical prose.

## Shared rules

- Preserve commands, identifiers, paths, links, hashes, counts, quoted errors, and user terminology exactly.
- State only facts supported by the task or current receipts. Mark uncertainty instead of smoothing it over.
- Keep detail that changes action or trust. Remove everything else.

Do not include hidden reasoning, routine progress, worker-by-worker narration, filler, boilerplate, or invented certainty.

## Agent briefs

A worker brief must stand alone. Include only:

```text
ID           stable unit identifier
GOAL         one bounded outcome
SCOPE        allowed and forbidden work
CONTEXT      required facts and artifact pointers
ACCEPTANCE   observable criteria
VERIFY       exact checks
TIMEBOX      stop point and retry budget
OUTPUT       artifact location and receipt shape
```

Use direct instructions. Point to source files instead of pasting broad context. Define unfamiliar terms once. Remove background that cannot change the worker's action.

## Review feedback

Lead with material findings ordered by consequence. For each actionable finding include the exact location, observable failure or continuing cost, trigger, evidence, and smallest corrective direction.

Do not narrate the diff, manufacture nits, praise routine work, repeat findings, expose internal reasoning, or include empty sections. If no material finding exists, say so plainly, give the verdict, and name the exact artifact and checks or lenses completed.

## Completion receipts

Include, in order:

1. The outcome in one sentence.
2. The strongest proof or artifact reference.
3. Meaningful deviations or residual risks.
4. A required user action only when a genuine gate remains.

For a large run, give receipt-derived totals and name only failed, abandoned, or blocked exceptions. Never turn `INCONCLUSIVE` into success.
