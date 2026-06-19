# Claude Cowork Lunch & Learn

A 1.5-hour hands-on workshop to get you up and running with Claude Cowork. You will leave with working AI workflows you can use next week.

## What you will build

| Exercise | Time | What you get |
|----------|------|-------------|
| **LinkedIn Content** | 20 min | A personal voice profile + your first AI-written LinkedIn post |
| **Meeting Intelligence** | 25 min | Pre-call briefs and post-meeting debriefs connected to your calendar, CRM, and enrichment tools |
| **Metaskills** | 20 min | A custom skill built from your most repetitive workflow |

## Prerequisites

Before the session, make sure you have:

1. **Claude Cowork** installed (desktop app or web app at [claude.ai/code](https://claude.ai))
2. **This repo cloned** or downloaded:
   ```bash
   git clone https://github.com/nodewin-labs/claude-cowork-lunch-learn.git
   ```
3. **3 to 5 writing samples** ready (LinkedIn posts, blog posts, emails, or any published writing in your voice)
4. Optional: accounts for the MCP integrations (see Exercise 2 workbook for details)

## How to install the plugins

### Option A: GitHub Connector (recommended)

Connect this repo to your Claude Cowork account and all plugins are discovered automatically:

1. Open **Claude Cowork** (desktop app or [claude.ai](https://claude.ai))
2. Go to **Settings → Integrations → GitHub**
3. Connect your GitHub account (or your company's GitHub org)
4. Search for `nodewin-labs/claude-cowork-lunch-learn`
5. Click **Install** — Claude discovers all 3 plugins from the marketplace.json

> **Screenshots**: See the `media/` folder for step-by-step installation screenshots.

### Option B: Manual folder install

If you prefer to install from a local clone:

1. Clone the repo:
   ```bash
   git clone https://github.com/nodewin-labs/claude-cowork-lunch-learn.git
   ```
2. In Claude Cowork, go to **Settings → Extensions → Add from folder**
3. Navigate to the plugin folder for each exercise:

| Exercise | Folder path |
|----------|------------|
| LinkedIn Content | `.claude/plugins/01-linkedin-content/` |
| Meeting Intelligence | `.claude/plugins/02-meeting-intelligence/` |
| Metaskills | `.claude/plugins/03-metaskills/` |

### MCP servers (Exercise 2)

The Meeting Intelligence plugin comes pre-configured with MCP server references for common tools. When you install the plugin, Claude will prompt you to connect the ones you use:

| Category | Supported tools |
|----------|----------------|
| **Calendar** | Google Calendar, Microsoft Outlook |
| **CRM** | HubSpot, Salesforce, Pipedrive, Teamleader |
| **Meeting recorder** | Fathom, Leexi, Krisp, Granola, Otter.ai, Fireflies |
| **Enrichment** | BrightData, FullEnrich |
| **Communication** | Gmail, Slack, Microsoft Teams |

You only need to connect the tools you actually use. The onboarding skill adapts to whatever is available.

## Repo structure

```
.claude/plugins/          — 3 installable plugin extensions (one per exercise)
workbooks/                — Step-by-step guides for each exercise
media/                    — Presentation slides (PNG)
```

## Workbooks

- [Session Guide](workbooks/session-guide.md) — Facilitator timeline
- [01 — LinkedIn Content](workbooks/01-linkedin-content.md)
- [02 — Meeting Intelligence](workbooks/02-meeting-intelligence.md)
- [03 — Metaskills](workbooks/03-metaskills.md)

## Enrichment tool setup (Exercise 2)

For the Meeting Intelligence exercise, you will optionally connect enrichment tools:

- **BrightData** — [Sign up here](https://get.brightdata.com/a9drujwubyjc) (5,000 free credits)
- **FullEnrich** — [Sign up here](https://fullenrich.partnerlinks.io/pum64ct0fe4h) (1,000 free credits)

Setup guides are in `.claude/plugins/02-meeting-intelligence/guides/`.

## About

Built by [Nodewin Labs](https://github.com/nodewin-labs) for the [Wintercircus](https://wintercircus.be) community. This is a recurring event — the repo is evergreen and updated between sessions.

## License

MIT
