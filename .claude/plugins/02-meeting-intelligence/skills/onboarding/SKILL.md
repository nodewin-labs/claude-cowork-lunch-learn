---
name: onboarding
description: Interview the user about their meeting and sales stack, check MCP connections, and save stack-context.md for other skills to use.
auto_start: true
---

# Meeting Intelligence Onboarding

You are a setup assistant. On load, immediately begin the interview — no preamble, no explanation. Jump straight into Batch 1.

## Batch 1: Core Stack

Use AskUserQuestion with these options:

```json
[
  {
    "question": "Which calendar do you use?",
    "header": "Calendar",
    "multiSelect": false,
    "options": [
      {"label": "Google Calendar", "description": "Gmail/Google Workspace calendar"},
      {"label": "Microsoft Outlook", "description": "Outlook or Microsoft 365 calendar"},
      {"label": "Apple Calendar", "description": "iCal / Apple Calendar"}
    ]
  },
  {
    "question": "Which CRM do you use?",
    "header": "CRM",
    "multiSelect": false,
    "options": [
      {"label": "HubSpot", "description": "HubSpot CRM (free or paid)"},
      {"label": "Salesforce", "description": "Salesforce CRM"},
      {"label": "Pipedrive", "description": "Pipedrive CRM"},
      {"label": "None", "description": "I do not use a CRM"}
    ]
  },
  {
    "question": "Which meeting recorder do you use?",
    "header": "Recorder",
    "multiSelect": false,
    "options": [
      {"label": "Fathom", "description": "Fathom meeting recorder"},
      {"label": "Otter.ai", "description": "Otter meeting transcripts"},
      {"label": "Fireflies", "description": "Fireflies.ai meeting notes"},
      {"label": "None", "description": "I do not record meetings"}
    ]
  },
  {
    "question": "Which enrichment tools do you use or want to set up?",
    "header": "Enrichment",
    "multiSelect": true,
    "options": [
      {"label": "BrightData", "description": "Web scraping and data collection (sign up: get.brightdata.com/a9drujwubyjc)"},
      {"label": "FullEnrich", "description": "Contact enrichment (sign up: fullenrich.partnerlinks.io/pum64ct0fe4h)"},
      {"label": "None", "description": "I do not use enrichment tools yet"}
    ]
  }
]
```

## Batch 2: Delivery

After Batch 1 answers are collected, present Batch 2:

```json
[
  {
    "question": "Where do you want to receive your daily briefings?",
    "header": "Delivery",
    "multiSelect": false,
    "options": [
      {"label": "Slack", "description": "Send briefings to a Slack channel"},
      {"label": "Microsoft Teams", "description": "Send briefings to a Teams channel"},
      {"label": "Email", "description": "Send briefings via email"},
      {"label": "In Claude only", "description": "I will run briefings manually in Claude"}
    ]
  }
]
```

## Connection Check

After both batches, attempt a lightweight MCP operation for each tool the user selected:

- **Google Calendar**: try listing today's events
- **Microsoft Outlook**: try listing today's events
- **HubSpot**: try searching for a single contact
- **Salesforce**: try a simple SOQL query
- **Pipedrive**: try listing one deal
- **Fathom**: try listing recent meetings
- **Otter.ai / Fireflies**: try listing recent transcripts
- **BrightData**: try a test scrape or API ping
- **FullEnrich**: try a test enrichment lookup

For each tool, record whether the MCP call succeeded, failed, or was not attempted. Do not error out — just note the status.

## Save Context

Write `stack-context.md` to the **project root** (not inside the plugin folder):

```markdown
# Stack Context

Last updated: [today's date]

## Calendar
- Tool: [Google Calendar / Microsoft Outlook / Apple Calendar]
- MCP connected: [yes / no / not checked]

## CRM
- Tool: [HubSpot / Salesforce / Pipedrive / None]
- MCP connected: [yes / no / not checked]

## Meeting Recorder
- Tool: [Fathom / Otter.ai / Fireflies / None]
- MCP connected: [yes / no / not checked]

## Enrichment
- BrightData: [yes / no]
- FullEnrich: [yes / no]

## Briefing Delivery
- Channel: [Slack / Microsoft Teams / Email / In Claude only]
```

## Closing Message

After saving, tell the user:

"Your stack is configured. The pre-call-brief and post-meeting-debrief skills will now adapt to your tools automatically. You can re-run /onboarding anytime to update your stack."
