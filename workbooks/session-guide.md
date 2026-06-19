# Session Guide — Claude Cowork Lunch & Learn (1.5h)

## Before the session

- [ ] Participants received setup instructions (README.md link)
- [ ] Participants have Claude Cowork installed
- [ ] Participants have 3-5 writing samples ready
- [ ] Presentation PNGs loaded in your deck
- [ ] This repo cloned on the facilitator laptop for live demo

## Timeline

### Block 1: Intro + Theory — Skills (15 min)

**12:00 — 12:15**

| Min | What | Notes |
|-----|------|-------|
| 0-3 | Welcome + housekeeping | Wi-Fi, repo URL on screen, quick poll: who has used Claude before? |
| 3-8 | What is Claude Cowork? | Show the interface. Explain: chat + projects + skills + memory |
| 8-12 | What are skills? | Show a SKILL.md file. Explain: triggers, auto-start, AskUserQuestion. Skills are instructions that make Claude an expert at one thing. |
| 12-15 | Bridge to Exercise 1 | "Let's build your first skill-powered workflow right now. Install Plugin 1." |

**Key slide**: media/01-what-are-skills.png

### Block 2: Exercise — LinkedIn Content (20 min)

**12:15 — 12:35**

| Min | What | Notes |
|-----|------|-------|
| 0-2 | Install Plugin 1 | Walk through: Settings → Extensions → Add from folder → `.claude/plugins/01-linkedin-content/` |
| 2-5 | Voice Builder starts | Auto-starts with interview. Participants fill in AskUserQuestion forms. |
| 5-10 | Optional website + writing samples | Those with a website URL paste it. Everyone pastes 3-5 writing samples. |
| 10-15 | Claude analyzes + writes about-me.md + voice.md | Show your screen while Claude works. Point out the analysis structure. |
| 15-18 | Run post-writer | Say "write a post" — Claude reads voice files, asks for topic, writes draft. |
| 18-20 | Share + react | 2-3 volunteers read their post hook aloud. Quick reactions. |

**Workbook**: workbooks/01-linkedin-content.md

### Block 3: Theory — MCPs (10 min)

**12:35 — 12:45**

| Min | What | Notes |
|-----|------|-------|
| 0-3 | What are MCPs? | Model Context Protocol = how Claude connects to external tools. Calendar, CRM, enrichment, meeting recorders. |
| 3-7 | Live demo: show MCP in action | Show a connected MCP (e.g., Google Calendar). Claude can now read your calendar. |
| 7-10 | Bridge to Exercise 2 | "Now let's connect YOUR tools and build a real meeting prep workflow." |

**Key slide**: media/02-what-are-mcps.png

### Block 4: Exercise — Meeting Intelligence (25 min)

**12:45 — 13:10**

| Min | What | Notes |
|-----|------|-------|
| 0-2 | Install Plugin 2 | `.claude/plugins/02-meeting-intelligence/` |
| 2-7 | Onboarding interview | Claude asks about their stack (calendar, CRM, recorder, enrichment). Saves stack-context.md. |
| 7-12 | Optional MCP setup | Those who want to connect BrightData/FullEnrich follow the guides. Others continue with what they have. |
| 12-20 | Run pre-call-brief | Claude reads stack-context.md, uses connected MCPs, generates a brief for their next meeting. |
| 20-25 | Discuss take-home | Explain: post-meeting-debrief skill, cron trigger for automated daily briefings. Show the workbook's take-home section. |

**Workbook**: workbooks/02-meeting-intelligence.md

### Block 5: Theory — Metaskills (10 min)

**13:10 — 13:20**

| Min | What | Notes |
|-----|------|-------|
| 0-3 | What are metaskills? | Skills that help you think (interview, problem-statement) and skills that BUILD skills (skill-creator). |
| 3-7 | Demo: skill-creator | Show Claude interviewing you about a workflow, then generating a SKILL.md. 2-min live demo. |
| 7-10 | Bridge to Exercise 3 | "Your turn. Think about your most repetitive task this week." |

**Key slide**: media/03-what-are-metaskills.png

### Block 6: Exercise — Metaskills (20 min)

**13:20 — 13:40**

| Min | What | Notes |
|-----|------|-------|
| 0-2 | Install Plugin 3 | `.claude/plugins/03-metaskills/` |
| 2-5 | Identify their workflow | Ask participants: "What is the thing you do every week that takes too long?" Give examples: weekly reports, client updates, invoice processing. |
| 5-15 | Claude interviews + generates skill | Claude uses interview methodology to understand the workflow, then skill-creator generates a SKILL.md. |
| 15-18 | Test the skill | Participants trigger their new skill and see it work. |
| 18-20 | Share | 2-3 volunteers share what skill they built. |

**Workbook**: workbooks/03-metaskills.md

### Close (5 min)

**13:40 — 13:45**

| Min | What | Notes |
|-----|------|-------|
| 0-2 | Recap | You now have: a voice profile, a meeting prep system, and a custom skill. All in Claude Cowork. |
| 2-4 | What's next | Claude Zero to Hero (full day) and Growth by Design (multi-day program). Share links/dates. |
| 4-5 | Q&A | Open floor. |

## Facilitator tips

- **Pacing**: If Exercise 2 runs long (MCP setup issues), cut the take-home discussion short. The workbook covers it.
- **Stragglers**: If someone can't install a plugin, pair them with a neighbor who has it working.
- **Writing samples**: Some people won't have samples ready. Tell them to use LinkedIn posts from someone they admire, or type "use samples" in voice-builder for defaults.
- **MCP failures**: Not every MCP will connect cleanly. That's fine — the onboarding skill handles graceful degradation. The brief still works with whatever is connected.
