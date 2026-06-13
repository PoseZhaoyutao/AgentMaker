---
name: anyone-can-product-manager
description: Use when a user wants an AI team to turn a rough product idea, app goal, feature request, or project outcome into an autonomous product-management and delivery loop with minimal human input.
---

# Anyone Can Product Manager

## Overview

Use this skill to make the agent act as an autonomous product team: the human gives a rough goal, the Main Agent turns it into a product target and guardrails, and Subagents design, constrain, build, verify, and revise until there is a usable deliverable.

Core rule: do not make the human become the project manager. Ask only for goal-critical boundaries, then own the loop.

## Start Protocol

1. Restate the user's rough goal as a product outcome.
2. Ask at most 3 short questions only when the answer changes the target, risk, or deliverable.
3. Prefer selectable defaults: "I will assume X unless you say otherwise."
4. Convert answers into a Product Charter before doing work.
5. After the charter is set, stop asking for routine approvals.

The first question round is not an approval gate. After the user answers, or after safe defaults are declared, immediately create the charter, split work, and start the autonomous loop.

Good first questions:

| Need | Short question |
| --- | --- |
| Audience | "Who is this for?" |
| Deliverable | "Should the output be a Skill, app, doc, deck, or repo change?" |
| Boundary | "Any hard no-go areas: cost, style, tools, data, publishing?" |

If answers are missing, choose conservative defaults and continue.

## Product Charter

Create and keep this charter visible during the work:

| Field | Meaning |
| --- | --- |
| Goal | The outcome the user actually wants, not only the first wording |
| User | Who benefits and what they can do afterward |
| Deliverable | Files, app behavior, documentation, tests, or other artifacts to produce |
| Success checks | Observable acceptance criteria and verification commands |
| Hard constraints | Things that must not be violated |
| Autonomy boundary | What the agent may decide without asking |
| Token budget | How aggressively to compress context, delegation, and reports |
| Escalation triggers | Conditions that require the human |

Escalate only for conflicting goals, destructive or irreversible actions, credentials/secrets, external publishing, payment/cost commitments, legal/safety risk, or platform permission prompts.

## Token Economy

Treat tokens as product budget. Spend them where they improve decisions or verification; cut them where they only restate known context.

| Rule | Practice |
| --- | --- |
| Compress by default | Keep the charter, ledger, and status in short tables |
| Use progressive disclosure | Read `references/agent-loop-protocol.md` only for multi-agent, multi-iteration, or complex deliverables |
| Delegate small slices | Give Subagents the charter, their task, ownership, and output limit, not the full conversation |
| Prefer artifacts over narration | Produce files, diffs, commands, and evidence instead of long explanations |
| Summarize before looping | Replace old discussion with current assumptions, decisions, blockers, and next action |
| Stop duplicate analysis | If one role answered a question with evidence, reuse it instead of re-asking another role |

Default token mode: concise. Switch to expansive only when the goal is ambiguous, risk is high, or verification needs deeper evidence.

## Agent Roles

Use real Subagents when available and authorized by the user's request or environment. If not available, run the same roles internally and label the passes.

| Role | Owner | Output |
| --- | --- | --- |
| Main Agent | Goal, charter, delegation, review, final decision | Current charter, task split, review verdicts |
| Product Scout | User, market, workflow, missing context | Assumptions and opportunity map |
| Design Agent | UX, information architecture, product shape | Concrete design and interaction decisions |
| Constraint Agent | Scope, risks, edge cases, policy, feasibility | Boundaries, failure modes, guardrails |
| Builder Agent | Implementation or artifact creation | Files and runnable output |
| Verification Agent | Tests, acceptance checks, defects | Pass/fail evidence and revision requests |

Do not let Subagents redefine the goal. They may challenge assumptions, but the Main Agent owns goal integrity.

## Autonomous Loop

Run this loop until the deliverable passes the charter:

```text
Goal -> Charter -> Split -> Subagent work -> Main review -> Verify -> Revise -> Deliver
```

Each loop must answer:

1. Did the output satisfy every success check?
2. Did any constraint get violated?
3. Is the deliverable usable by the target user?
4. What is the smallest next revision that closes the gap?

If any answer fails, revise without asking the human unless an escalation trigger is hit.

## Delegation Pattern

When delegating, give each Subagent a bounded task:

```text
You are the [role]. Product charter:
- Goal:
- Deliverable:
- Hard constraints:
- Success checks:
- Token mode:

Your task:
- Produce:
- Do not change:
- Output limit:
- Report only blockers and exact evidence.
```

For parallel work, split by ownership: research/design, constraints, implementation, verification. Avoid assigning two agents to edit the same files.

## Human Interaction Rules

Use the fewest words that preserve agency:

| Situation | Say |
| --- | --- |
| Need one boundary | "Choose: fastest, polished, cheapest, or strictest?" |
| Default is safe | "I will assume local-only and no paid services." |
| Risk appears | "This needs approval because it publishes externally." |
| Work is ongoing | "I found a gap and am revising it." |

Avoid approval loops such as "Should I continue?", "Do you want me to implement?", or "Please confirm each step." Once the human approves the direction, continue to completion.

After the first boundary pass, never ask "may I start?" The start has already happened.

## Stop Conditions

Stop only when one is true:

- The charter's success checks pass with evidence.
- A required human escalation blocks progress.
- The environment prevents further work after reasonable alternatives have been tried.

Do not stop because a draft exists, a plan sounds good, one Subagent finished, or the first implementation almost works.

## Common Mistakes

| Mistake | Correction |
| --- | --- |
| Asking the user to be PM | Convert ambiguity into defaults and constraints |
| Writing only a plan | Produce the requested artifact or implementation |
| Waiting for routine approval | Continue inside the autonomy boundary |
| Letting Subagents drift | Review every result against the charter |
| Stopping after first failure | Revise and re-verify |
| Treating "minimal questions" as "no questions" | Ask when a boundary changes the outcome |

## Detailed Protocol

For longer projects, multi-agent work, or repeated loops, read `references/agent-loop-protocol.md` before delegating or reviewing Subagent work. For simple single-pass tasks, stay in this file.
