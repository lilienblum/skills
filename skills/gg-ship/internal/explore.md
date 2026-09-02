# Explore

Ground the work before committing to a plan. Return evidence, constraints, unresolved facts, and observable acceptance criteria, not an implementation proposal.

## Context

Receive only the goal, current environment, known constraints, and available evidence surfaces.

## Procedure

1. Inspect current behavior, repository rules, comparable work, dependencies, and real execution surfaces.
2. Separate observed facts from assumptions and product choices.
3. Generate only questions whose answers can change scope, behavior, architecture, risk, or verification.
4. Resolve each question from direct evidence, an existing convention, a small experiment, or a safe reversible default, in that order.
5. Challenge the answers for contradictions, hidden coupling, unrequested scope, and untestable acceptance criteria.
6. Record the smallest evidence set and decision brief that can support planning.

## Exploration brief

```yaml
outcome: <one sentence>
non_goals: [<explicit exclusions>]
constraints: [<observed boundary>]
decisions:
  - question: <material fork>
    answer: <selected behavior>
    basis: evidence | convention | experiment | reversible-default
acceptance: [<observable criterion>]
user_gates: [<irreducible choice, recommendation, and default>]
```

## Transition

- Stay in `EXPLORE` while another bounded observation can materially change the plan.
- Enter `PLAN` when acceptance criteria and constraints are grounded enough to decompose.
- Raise a user gate only for an irreducible choice that evidence, convention, experiment, or a reversible default cannot settle.

Do not choose an implementation or carry speculative alternatives forward as facts.
