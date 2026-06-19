---
name: voice-builder
description: >
  Build a personalised voice profile from a short interview and writing samples. Use at the start of any project where you want Claude to learn who you are and how you write. Trigger with "build my voice", "learn my voice", "set up my content system", or when dropping writing samples into chat. Produces about-me.md and voice.md in the project root.
---

# Voice Builder

## What this skill produces

Two files in the project root:

1. **about-me.md**: WHO you are — name, role, audience, topic pillars, point of view, brand promise
2. **voice.md**: HOW you write — tone, rhythm, hooks, vocabulary, sentence patterns, absence signals

## CRITICAL: Auto-start on load

The moment this skill is loaded or triggered, go straight to Step 1. No summary, no explanation, no preamble. Data-first.

## Step 1. Optional website analysis

Say this as your very first message:

> To build your voice profile, I can start by analyzing your website or blog. This gives me a head start on your brand, tone, and content topics.
>
> **Paste your website or blog URL below, or type "skip" to go straight to the interview.**

If the user provides a URL:
1. Fetch the homepage and blog page using WebFetch or defuddle
2. Extract: brand promise, 3-5 sub-promises/values, tone, vocabulary patterns, brand personality
3. Present a summary and ask for confirmation
4. Store the results for use in about-me.md

If the user types "skip": proceed directly to Step 2.

## Step 2. Run the About Me interview

Use AskUserQuestion in 2 batches. The tool renders interactive forms — better than typing answers in chat.

### Batch 1 (send immediately after Step 1)

```json
[
  {
    "question": "What is your name and what do you do?",
    "header": "About you",
    "multiSelect": false,
    "options": [
      {"label": "Founder", "description": "I run my own company or consultancy"},
      {"label": "Marketing lead", "description": "I lead marketing at a company"},
      {"label": "Sales leader", "description": "I lead a sales team or run business development"},
      {"label": "Consultant", "description": "I advise companies on strategy or operations"}
    ]
  },
  {
    "question": "Who are you writing for?",
    "header": "Audience",
    "multiSelect": false,
    "options": [
      {"label": "Founders and CEOs", "description": "Decision makers running companies"},
      {"label": "B2B buyers", "description": "People evaluating products or services for their company"},
      {"label": "Tech leaders", "description": "CTOs, VPs of engineering, technical decision makers"},
      {"label": "Small business owners", "description": "Entrepreneurs and SME operators"}
    ]
  },
  {
    "question": "What are the 3 to 5 topics you want to be known for?",
    "header": "Topics",
    "multiSelect": true,
    "options": [
      {"label": "AI and automation", "description": "How AI tools change work"},
      {"label": "Go-to-market strategy", "description": "Sales, marketing, growth tactics"},
      {"label": "Leadership", "description": "Management, hiring, culture, team building"},
      {"label": "Sales intelligence", "description": "Data-driven selling, CRM, prospecting"}
    ]
  },
  {
    "question": "What is your point of view on your industry — the thing you believe that others do not?",
    "header": "Hot take",
    "multiSelect": false,
    "options": [
      {"label": "Most advice is wrong", "description": "The consensus in your industry is broken"},
      {"label": "People overcomplicate it", "description": "The answer is simpler than people think"},
      {"label": "A big shift is coming", "description": "Something is about to change and most are not ready"}
    ]
  }
]
```

### Batch 2 (send immediately after Batch 1 answers, no commentary between)

```json
[
  {
    "question": "What is the one thing you want people to think when they see your name?",
    "header": "Brand promise",
    "multiSelect": false,
    "options": [
      {"label": "This person is practical", "description": "They give me things I can use immediately"},
      {"label": "This person is honest", "description": "They tell me what others will not"},
      {"label": "This person is ahead", "description": "They see what is coming before everyone else"}
    ]
  },
  {
    "question": "What is one thing you refuse to write about?",
    "header": "Off limits",
    "multiSelect": false,
    "options": [
      {"label": "Politics", "description": "No political takes, ever"},
      {"label": "Personal life", "description": "Keep it professional only"},
      {"label": "Competitors", "description": "No naming or shaming other people or brands"}
    ]
  }
]
```

After both batches: if any answer is blank, ask once more in chat, then move on.

## Step 3. Write about-me.md

Create about-me.md in the project root:

```
# About Me

## Name and role
[From question 1]

## Audience
[From question 2, expanded into 2-3 sentences]

## Topic pillars
[3-5 topics from question 3, one line each]

## Point of view
[From question 4, written as a clear statement]

## Brand promise
[From question 5]

## Off limits
[From question 6]
```

If website analysis was done in Step 1, enrich with: brand promise from website, sub-promises, and tone baseline.

Keep under 300 words.

## Step 4. Ask for writing samples

> Now paste 3 to 5 pieces of writing you want me to learn from. LinkedIn posts, blog posts, emails, tweets, or any published writing. One piece per message or all at once.
>
> If you do not have samples ready, type "use samples" for a starter set you can swap later.

Wait for minimum 3 samples. If fewer, ask for more.

## Step 5. Analyse the samples

Read every sample. Extract patterns across ALL samples:

**Voice signals**: average sentence length, paragraph rhythm, hook style, POV, tone, signature phrases, closing style

**Structural signals**: length range, lists vs prose, transitions

**Topic signals**: recurring subjects, apparent audience

**Absence signals**: words/punctuation consistently absent, hook types never used, tones never hit, structures avoided

## Step 6. Write voice.md

Create voice.md in the project root:

```
# Voice Profile

## Who I sound like
[2-3 sentences describing the overall voice]

## Tone
[3-5 attributes the voice hits, plus 1-2 tones it never hits]

## Sentence rhythm
[Average length, pacing, paragraph structure, avoidance patterns]

## Hook patterns
[3-5 hook types with one example each, plus absent hook types]

## How I open
[1-2 sentences, note opening moves the voice avoids]

## How I close
[1-2 sentences, include CTA style]

## Signature phrases
[Recurring words or phrases]

## Off-limits
[Words, punctuation, or constructions absent from every sample]

## What this voice never does
[3-5 specific behaviours from gaps in the samples]
```

Fill every section from actual data. No generic filler. Keep under 500 words.

## Step 7. Confirm and hand off

> Your voice profile is built. Two files are now in your project: about-me.md and voice.md.
>
> You are ready to go. Say "write a post" to draft a LinkedIn post in your voice.

## Rules

- Auto-start on load. No summary, no preamble.
- Output files in code blocks for easy copy-paste.
- Work from what is in the samples. Do not invent patterns.
- Minimum 3 samples for pattern detection.
- If samples contradict, note the contradiction rather than smoothing it.
- Keep about-me.md under 300 words, voice.md under 500 words.
- British English unless samples are clearly American.
- Never use em dashes in any output.
