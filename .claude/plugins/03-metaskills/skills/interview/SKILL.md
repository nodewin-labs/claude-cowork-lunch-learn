---
name: interview
description: "Interview me until 95% confidence about what I actually want — not what I think I should want. Use when starting new work, scoping a task, or when intent is ambiguous."
---

# Intent Interview

## Phase 1: Interview

Load `references/interview-methodology.yaml` and apply the layered questioning approach.

Interview me until you have 95% confidence about what I actually want — not what I think I should want. This means:

1. **Don't accept the first framing.** Users present solutions, not problems. Dig to Layer 2 (motivation) before accepting anything.
2. **Challenge assumptions at Layer 4.** Push back. Say "I think you're solving the wrong problem" if that's what you believe. Use the flip/delete/10x tests.
3. **Track confidence explicitly.** Each Q&A has a confidence_delta. If you're gaining <5% per question, you're asking the wrong questions — go deeper, not wider.
4. **Don't ask what you can look up.** Never ask about file paths, existing code, or system state. Only interview about intent, constraints, and preferences.
5. **Probe out-of-scope proactively.** Before restating, suggest what should be OUT of scope. Users don't think about boundaries until you name them.

Only after 95% confidence: RESTATE using the Layer 5 format from the methodology, and wait for explicit approval.

## Phase 2: Route Decision

After the interview is approved, determine the nature of the work:

**Route A — Problem-shaped** (ambiguity, multiple possible approaches, trade-offs):
- Suggest: "This feels problem-shaped — use /problem-solution for structured analysis."

**Route B — Task-shaped** (clear scope, known approach, execution-ready):
- Say: "Interview complete. You have a clear brief — ready to execute."

Use your judgement. If in doubt, ask: "This feels [problem-shaped / task-shaped] — should I run /problem-solution for structured analysis, or go straight to execution?"
