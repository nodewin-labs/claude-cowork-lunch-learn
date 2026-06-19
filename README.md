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

Each exercise has its own Claude Cowork plugin. Install them one at a time as the session progresses:

**Exercise 1 — LinkedIn Content:**
```
Open Claude Cowork → Settings → Extensions → Add from folder → .claude/plugins/01-linkedin-content/
```

**Exercise 2 — Meeting Intelligence:**
```
Open Claude Cowork → Settings → Extensions → Add from folder → .claude/plugins/02-meeting-intelligence/
```

**Exercise 3 — Metaskills:**
```
Open Claude Cowork → Settings → Extensions → Add from folder → .claude/plugins/03-metaskills/
```

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
