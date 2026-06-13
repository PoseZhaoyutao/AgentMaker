# AgentMaker

This repository contains the `anyone-can-product-manager` Skill, displayed as "普通人也能做产品经理".

The Skill turns a rough product idea into an autonomous product-management loop: the human gives a goal and hard boundaries, the Main Agent keeps the Product Charter and review loop, and Subagents handle discovery, design, constraints, building, verification, and revision until the deliverable passes.

## Contents

```text
skills/
  anyone-can-product-manager/
    SKILL.md
    agents/
      ai.yaml
    references/
      agent-loop-protocol.md
```

## Core Ideas

- Minimal human input: ask only goal-critical boundary questions.
- Main Agent owns the goal, charter, delegation, review, and final decision.
- Subagents work on scoped slices: scout, design, constraint, build, verify.
- The loop continues until success checks pass or a real escalation trigger blocks progress.
- Token economy is built in: short charters, compressed state, bounded Subagent outputs, and progressive disclosure.

## Usage

Invoke the Skill with:

```text
Use $anyone-can-product-manager to turn my rough product goal into an autonomous build loop.
```

The Skill starts by restating the user's rough goal as a product outcome, asks up to three short boundary questions when needed, creates a Product Charter, then runs the autonomous loop.

## Validation

Validate the Skill structure with:

```powershell
python "C:\Users\admin\.codex\skills\.system\skill-creator\scripts\quick_validate.py" "skills\anyone-can-product-manager"
```

Expected output:

```text
Skill is valid!
```
