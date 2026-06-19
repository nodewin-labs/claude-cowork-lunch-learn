# Exercise 2: Meeting Intelligence

Connect your meeting stack and get AI-powered pre-call briefs and post-meeting debriefs.

## Prerequisites

- [ ] Claude Cowork installed and open
- [ ] Plugin 02 installed: Settings → Extensions → Add from folder → `.claude/plugins/02-meeting-intelligence/`
- [ ] Know which calendar, CRM, and meeting recorder you use
- [ ] Optional: BrightData account ([sign up — 5,000 free credits](https://get.brightdata.com/a9drujwubyjc))
- [ ] Optional: FullEnrich account ([sign up — 1,000 free credits](https://fullenrich.partnerlinks.io/pum64ct0fe4h))

## What you will build

1. **stack-context.md** — Your personalized tool configuration (which calendar, CRM, recorder, enrichment tools)
2. **A pre-call brief** — AI-generated meeting preparation with attendee profiles, past interactions, and talking points
3. **Take-home**: post-meeting debrief skill + automated daily briefing via cron trigger

## Steps

### Step 1: Run the onboarding interview

The onboarding skill auto-starts. Claude will ask about your tools:

1. **Calendar**: Google Calendar, Outlook, or Apple Calendar
2. **CRM**: HubSpot, Salesforce, Pipedrive, or none
3. **Meeting recorder**: Fathom, Otter, Fireflies, or none
4. **Enrichment tools**: BrightData, FullEnrich, or none
5. **Briefing delivery**: Slack, Teams, Email, or manual

Claude will check which MCP servers are connected and save everything to `stack-context.md`.

### Step 2: Connect MCP servers (optional, 5 min)

If you want richer briefings, connect one or more MCP servers:

**Google Calendar MCP:**
- Settings → MCP Servers → Add → Search "Google Calendar" → Connect your Google account

**HubSpot MCP:**
- Settings → MCP Servers → Add → Search "HubSpot" → Connect with your HubSpot API key

**BrightData MCP:**
- Follow the guide at `.claude/plugins/02-meeting-intelligence/guides/brightdata-mcp-setup.md`

**FullEnrich MCP:**
- Follow the guide at `.claude/plugins/02-meeting-intelligence/guides/fullenrich-mcp-setup.md`

After connecting, re-run onboarding to update your stack-context.md.

### Step 3: Run a pre-call brief

Say "prepare me for my next meeting" or "pre-call brief."

Claude will:
1. **Find your meeting** — via calendar MCP or ask you to paste meeting details
2. **Research attendees** — via enrichment MCPs (LinkedIn profiles, company info) or skip if no enrichment connected
3. **Check past interactions** — via CRM MCP (deals, notes, history) or skip if no CRM
4. **Check past recordings** — via meeting recorder MCP (previous conversations) or skip if no recorder
5. **Generate the brief** — structured output with Meeting Context, Attendee Profiles, Past Interactions, and Talking Points

The brief adapts to whatever tools you have connected. No tools? You still get a useful brief based on whatever context you can paste in.

### Step 4: Review the brief

Read through the brief. Ask Claude to:
- "Add more context about [person]"
- "What should I avoid discussing?"
- "Suggest 3 opening questions"

## Verification

- [ ] stack-context.md exists in your project root with your tool configuration
- [ ] You have a pre-call brief for an upcoming meeting
- [ ] The brief includes at least meeting context and talking points
- [ ] If MCPs are connected, the brief includes data from those tools

## Take-home

### Post-meeting debrief

After your next real meeting, come back and say "debrief my meeting." Claude will:
- Pull the transcript (if recorder is connected)
- Extract key decisions, action items, and follow-ups
- Suggest CRM updates
- Compare what was discussed vs. what was planned in the pre-call brief

### Automated daily briefings (advanced)

Set up a cron trigger to run pre-call briefs automatically:

1. In Claude Cowork, go to Settings → Schedules
2. Create a new schedule:
   - **Name**: "Daily meeting prep"
   - **Trigger**: Every weekday at 7:00 AM
   - **Prompt**: "Run pre-call-brief for all meetings today. Send the briefing to [your delivery channel from onboarding]."
3. Claude will run the brief and send it to your Slack, Teams, or email each morning.

This requires MCP servers for calendar and delivery channel to be connected.
