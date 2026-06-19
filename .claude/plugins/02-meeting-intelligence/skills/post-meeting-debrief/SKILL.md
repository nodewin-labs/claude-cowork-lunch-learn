---
name: post-meeting-debrief
description: >
  Generate an AI-powered post-meeting debrief after a meeting. Pulls transcripts if available, extracts key decisions, action items, and suggests CRM updates. Adapts to your connected tools. Requires stack-context.md — run /onboarding first. Trigger with "debrief my meeting", "post-meeting brief", or "meeting debrief".
---

# Post-Meeting Debrief

## Prerequisites

Read `stack-context.md` from the project root. If missing, tell the user: "Run /onboarding first to configure your meeting stack." Then stop.

## Step 1. Identify the meeting

**If meeting recorder MCP is connected:**
- List recent meetings from the recorder
- Present via AskUserQuestion and let the user pick one
- Pull the full transcript

**If no recorder MCP:**
- Ask: "Which meeting do you want to debrief? Paste the transcript, your notes, or describe what happened."

Also check if a pre-call brief exists for this meeting (search for markdown files with matching attendee names or date).

## Step 2. Extract key information

From the transcript or notes, extract:

**Decisions made:**
- What was agreed on? Who committed to what?

**Action items:**
- Who needs to do what, by when?
- Distinguish YOUR action items from THEIR action items

**Key insights:**
- Surprising information that came up
- Concerns or objections raised
- Opportunities identified

**Relationship signals:**
- How engaged were the attendees?
- Any rapport builders or tension points?
- Who was the decision maker vs influencer?

## Step 3. Cross-reference with pre-call brief

If a pre-call brief exists for this meeting:
- Compare planned talking points vs what was actually discussed
- Note any planned topics that were NOT covered (follow-up needed?)
- Highlight new topics that emerged unexpectedly

## Step 4. Check CRM context

**If CRM is connected:**
- Pull current deal stage, notes, and activity history
- Suggest specific CRM updates based on the meeting:
  - Deal stage change?
  - New notes to add?
  - Follow-up task to create?
  - Contact properties to update?

**If no CRM:** Skip this section.

## Step 5. Generate the debrief

```
# Post-Meeting Debrief

## Meeting
- **Title**: [meeting title]
- **Date**: [date]
- **Attendees**: [names]
- **Duration**: [if known]

## Key Decisions
1. [Decision + who made it]
2. [Decision + who made it]

## Action Items

### Your action items
- [ ] [Task] — by [date if mentioned]
- [ ] [Task]

### Their action items
- [ ] [Person]: [Task] — by [date if mentioned]
- [ ] [Person]: [Task]

## Key Insights
- [Insight 1]
- [Insight 2]
- [Insight 3]

## Planned vs Actual
[Only if pre-call brief exists]
- **Covered**: [topics from the brief that were discussed]
- **Missed**: [planned topics not covered — follow up needed]
- **New**: [topics that came up unexpectedly]

## Suggested CRM Updates
[Only if CRM is connected]
- **Deal stage**: [current → suggested]
- **Notes to add**: [summary of key discussion points]
- **Follow-up task**: [next step + date]

## Next Steps
1. [Most important follow-up action]
2. [Second priority]
3. [Third priority]
```

## Step 6. Refine

> Anything to add or correct? Or should I save this debrief?

If approved, save as markdown. Offer to draft a follow-up email if relevant.

## Rules

- Always read stack-context.md before starting
- Gracefully skip any tool not connected
- Never fabricate meeting content — only use actual transcript/notes
- Action items must have clear owners
- Keep the debrief actionable — every section should drive a next step
