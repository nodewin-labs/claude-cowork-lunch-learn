---
name: problem-solution
description: >
  Find structured solutions for a confirmed problem. Activates after the user confirms a problem statement. Runs context analysis, forward projection, dependency mapping, and reverse engineering, then delegates to /compare-options for evaluation.
---

# Problem Solution

Structured solution finding for a confirmed problem.

## Prerequisites

The problem must be confirmed. If no confirmed problem exists in the conversation, ask: "What is the confirmed problem we are solving?" Do not proceed without clarity.

## Process

### Wave 1 — Context + Vision (parallel)

Run these two phases simultaneously:

**Phase 1 — Context Analysis**
Load `references/phase1-context-analysis.yaml`. Gather background, evidence, relevance, and impact. Check assumptions against facts.

**Phase 2 — Forward Projection**
Load `references/phase2-forward-projection.yaml`. Define the desired end state — what does "solved" look like concretely?

### Wave 2 — Dependencies (sequential)

**Phase 3 — Dependency Mapping**
Load `references/phase3-dependency-mapping.yaml`. Now that you know both current context AND desired state, map upstream + downstream dependencies, identify blockers and critical path.

### Wave 3 — Reverse Engineering (sequential)

**Phase 4 — Reverse Engineering**
Load `references/phase4-reverse-engineering.yaml`. Work backwards from goal through the dependency chain to the current state. Produces the natural execution order.

### Wave 4 — Option Evaluation

Generate 2-3 solution options based on the reverse-engineered path. For each option, describe:
- How it works (1-2 sentences)
- What it requires
- Key trade-offs

Then delegate to /compare-options for structured evaluation.

Use AskUserQuestion after evaluation to confirm which option the user wants.

### Wave 5 — Solution Roadmap

After the user picks an option, produce the execution plan:

```
## Solution Roadmap

**Selected approach:** [option name]

### Steps
1. [Step] — [what and why]
2. [Step] — [what and why]
3. [Step] — [what and why]

### Dependencies
- [Step X] must complete before [Step Y]

### Success criteria
- [ ] [Criterion 1]
- [ ] [Criterion 2]

### Risks
- [Risk] — mitigation: [approach]
```

Present to the user for approval.

## Output

Always produce visual markdown. Use tables, lists, and structured sections. The user should scan the full assessment in under 2 minutes.

## Rules

- Wave 1 phases run in parallel.
- Never skip Phase 3 (dependencies). Most failed solutions fail because of missed deps.
- Phase 4 depends on Phase 3 — do not start before deps are mapped.
- Wave 4 delegates to /compare-options — do not reinvent option evaluation.
- Be assertive in recommendations. "It depends" is not an answer.

## Decision Funnel

```
/problem-statement  →  /problem-solution      →  /compare-options (Wave 4)
  "WHAT is wrong?"      "HOW do we solve it?"      "WHICH option?"
```
