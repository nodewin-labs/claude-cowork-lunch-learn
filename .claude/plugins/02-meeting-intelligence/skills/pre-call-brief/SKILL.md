---
name: pre-call-brief
description: >
  Generate an AI-powered pre-call brief for an upcoming meeting. Adapts to your connected tools (calendar, CRM, meeting recorder, enrichment). Requires stack-context.md in the project root — run /onboarding first. Trigger with "prepare me for my meeting", "pre-call brief", or "meeting prep".
---

# Pre-Call Brief

## Prerequisites

Read `stack-context.md` from the project root. If missing, tell the user: "Run /onboarding first to configure your meeting stack." Then stop.

## Step 1. Identify the meeting

Based on stack-context.md:

**If calendar MCP is connected:**
- Query the calendar for upcoming meetings (today or this week)
- Present the list via AskUserQuestion and let the user pick one
- Extract: meeting title, time, attendees (names + emails), description/agenda

**If no calendar MCP:**
- Ask the user: "Paste your meeting details — who are you meeting, when, and what is it about?"
- Extract the same fields from their response

## Step 2. Research attendees

For each attendee, gather context using available tools:

**If enrichment tools are connected (BrightData/FullEnrich):**
- Look up LinkedIn profiles for each attendee
- Extract: current role, company, recent activity, mutual connections
- Summarize key talking points from their profile

**If CRM is connected (HubSpot/Salesforce/Pipedrive):**
- Search for each attendee in the CRM
- Extract: contact record, associated company, deals, notes, last interaction
- Note any open deals or recent communications

**If meeting recorder is connected (Fathom/Otter/Fireflies):**
- Search for past meetings with these attendees
- Extract: key topics discussed, decisions made, action items from previous conversations

**If none of the above:**
- Ask the user: "What do you already know about these people? Any LinkedIn URLs, past context, or notes?"
- Work with whatever they provide

## Step 3. Generate the brief

Produce a structured brief:

```
# Pre-Call Brief

## Meeting
- **Title**: [meeting title]
- **Date/Time**: [date and time]
- **Duration**: [if known]

## Attendees
[For each attendee:]
### [Name]
- **Role**: [title at company]
- **Company**: [company name]
- **Key context**: [2-3 bullet points from enrichment/CRM/past meetings]
- **LinkedIn**: [URL if found]

## Past Interactions
[Summary of previous meetings, CRM notes, or communications with these people. If none available, state "No prior interactions found."]

## Meeting Context
[What this meeting appears to be about, based on calendar description and attendee profiles]

## Talking Points
1. [Suggested opening based on shared context or recent activity]
2. [Key question to ask based on their role/company]
3. [Topic to explore based on past interactions]
4. [Potential value you can offer based on their pain points]

## Watch Out For
- [Anything to be aware of — competing priorities, sensitive topics, timing considerations]
```

## Step 4. Refine

Ask the user:
> Anything to add or adjust? Or is this brief ready to go?

If feedback, update and regenerate. If approved, save as a markdown file.

## Rules

- Always read stack-context.md before starting
- Gracefully skip any tool that is not connected — never error on missing MCPs
- The brief should be useful even with zero MCPs connected (user-provided context only)
- Keep the brief scannable — bullet points over paragraphs
- Do not fabricate attendee information — only include what tools actually return
