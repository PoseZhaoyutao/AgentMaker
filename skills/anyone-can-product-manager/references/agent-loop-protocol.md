# Agent Loop Protocol

Use this reference when the task needs multiple agents, multiple iterations, or a non-trivial deliverable.

## Loop Ledger

Maintain a compact ledger in the working notes:

| Field | Content |
| --- | --- |
| Charter version | v1, v2, etc. |
| Active assumptions | Defaults chosen without asking the user |
| Open risks | Risks not yet eliminated |
| Subagent queue | Role, task, file ownership, status |
| Verification evidence | Commands, checks, screenshots, reviews |
| Context budget | Concise, normal, or expansive |
| Compressed state | Current facts, decisions, blockers, next action |
| Next revision | Smallest concrete action to improve fit |

Update the ledger after every review cycle.

## Context Compression

Before each loop, compress history into:

```text
Goal:
Decisions:
Assumptions:
Open blockers:
Changed files/artifacts:
Verification evidence:
Next action:
```

Use the compressed state for future prompts. Do not paste long prior discussion unless exact wording matters.

## Charter Review

Before each delegation round, the Main Agent checks:

1. The goal is still phrased as an outcome.
2. Success checks are observable.
3. Constraints are hard enough to prevent unsafe autonomy.
4. Subagent tasks do not overlap destructively.
5. Token mode fits the risk: concise for routine work, expansive for ambiguity or high risk.

If the charter is vague, improve it. Do not ask the user unless the ambiguity changes a hard boundary.

## Subagent Review Rubric

Score each Subagent output:

| Score | Meaning | Action |
| --- | --- | --- |
| Pass | Meets charter and gives evidence | Integrate |
| Partial | Useful but incomplete | Assign focused revision |
| Drift | Optimizes a different goal | Reject and restate charter |
| Risk | Violates boundary or creates unsafe action | Escalate or redesign |

The Main Agent must synthesize, not merely concatenate, Subagent outputs.

## Subagent Token Budgets

Set explicit output limits:

| Task | Default limit |
| --- | --- |
| Scout or design pass | 10 bullets or fewer |
| Constraint pass | Risks table with top 5 items |
| Builder pass | Changed files plus key choices |
| Verification pass | Checks run, result, failures only |
| Revision request | One failed check and one fix target |

Ask for full reasoning only when the Main Agent cannot judge correctness from evidence.

## Verification Requirements

Choose checks that match the deliverable:

- Code: targeted tests, lint/typecheck/build, manual smoke where useful.
- App/UI: browser run, screenshot or interaction check, responsive sanity check.
- Document/Skill: structure validation, trigger clarity, pressure scenario, forward-test when practical.
- Research/strategy: source quality, assumption table, contradiction scan, decision recommendation.

Verification must produce evidence. "Looks good" is not evidence.

## Revision Policy

When verification fails:

1. Name the exact failed check.
2. Assign the smallest fix to the right owner.
3. Re-run the failed check.
4. Repeat until pass or escalation.
5. Carry forward only the compressed state and fresh evidence.

Do not broaden scope during revision unless the current approach cannot satisfy the charter.

## Escalation Policy

Ask the human only when:

- Two or more required goals conflict.
- The next action is destructive, irreversible, external, paid, credentialed, legally sensitive, or outside available permissions.
- The target user, deliverable, or hard boundary cannot be inferred safely.
- Three consecutive loop iterations fail for the same blocker and no meaningful alternative remains.

Escalation format:

```text
Blocked by: [specific condition]
Why it matters: [risk to goal or boundary]
Smallest decision needed: [one short choice]
Default if allowed: [recommended path]
```

## Final Delivery

Finish with:

- What was produced.
- Where the artifact or files are.
- Evidence that success checks passed.
- Remaining risks or explicit blocked items.

Do not end with a generic "tell me if you want more." Offer a concrete next move only when it naturally extends the charter.
