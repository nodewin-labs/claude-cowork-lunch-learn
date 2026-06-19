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

Use AskUserQuestion for each question. **Build the options dynamically** from the website analysis in Step 1 — the suggestions should reflect what you actually found on their site. Always include an "Other" option so the user can nuance or provide their own answer if the suggestions do not fit.

If Step 1 was skipped (no website analysis), use generic open-ended options instead.

### How to build dynamic options

For each question below, generate 2-3 option labels and descriptions **derived from the website analysis**. For example:
- If the website says "We help B2B SaaS companies grow" → suggest "B2B SaaS founders" as an audience option
- If the blog covers AI, sales, and leadership → suggest those as topic options
- If the website tone is blunt and data-driven → suggest "Blunt and data-driven" as a brand promise option

The "Other" option is always available automatically via AskUserQuestion — the user can type their own answer.

### Batch 1 (send immediately after Step 1)

Call AskUserQuestion with 3-4 questions. Build the options dynamically:

```json
[
  {
    "question": "What is your name and what do you do? Describe your role and what makes it different.",
    "header": "About you",
    "multiSelect": false,
    "options": [
      {"label": "[role suggested from website, e.g. 'Founder at X']", "description": "[context from website about what the company does]"},
      {"label": "[alternative role interpretation]", "description": "[based on website signals]"}
    ]
  },
  {
    "question": "Who is your audience? When you publish on LinkedIn, who do you want reading it?",
    "header": "Audience",
    "multiSelect": false,
    "options": [
      {"label": "[audience from website, e.g. 'B2B SaaS founders']", "description": "[why — based on website value prop]"},
      {"label": "[secondary audience from website]", "description": "[based on blog content or services page]"}
    ]
  },
  {
    "question": "What are the 3 to 5 topics you want to be known for?",
    "header": "Topics",
    "multiSelect": true,
    "options": [
      {"label": "[topic 1 from blog/website]", "description": "[specific angle found on site]"},
      {"label": "[topic 2 from blog/website]", "description": "[specific angle found on site]"},
      {"label": "[topic 3 from blog/website]", "description": "[specific angle found on site]"}
    ]
  },
  {
    "question": "What is your point of view — the thing you believe that most people in your space do not?",
    "header": "Hot take",
    "multiSelect": false,
    "options": [
      {"label": "[contrarian angle from website messaging]", "description": "[extracted from how they position against alternatives]"},
      {"label": "[another distinctive stance from blog content]", "description": "[based on recurring themes]"}
    ]
  }
]
```

### Batch 2 (after Batch 1 answers are confirmed)

```json
[
  {
    "question": "What is the one thing you want people to think when they see YOUR name? Not your company — you personally.",
    "header": "Brand promise",
    "multiSelect": false,
    "options": [
      {"label": "[brand personality from website tone analysis]", "description": "[e.g. 'Practical — gives things I can use immediately']"},
      {"label": "[alternative brand impression]", "description": "[based on website voice signals]"}
    ]
  },
  {
    "question": "What topics or angles do you refuse to write about, no matter how trendy?",
    "header": "Off limits",
    "multiSelect": false,
    "options": [
      {"label": "[inferred from website absence patterns]", "description": "[e.g. 'No political takes — not found anywhere on site']"},
      {"label": "[another boundary inferred from tone]", "description": "[based on what the website deliberately avoids]"}
    ]
  }
]
```

### After both batches

Review each answer for depth. If any answer is too brief or generic to build a meaningful profile, probe deeper with a follow-up AskUserQuestion:

- **Too-brief role**: "Can you tell me more? What does your day-to-day look like, and what makes your role different from the average [title]?"
- **Vague audience**: "Think of one specific person — what is their role, what keeps them up at night?"
- **Broad topics**: "Can you narrow each one? Not 'marketing' but 'how small teams punch above their weight with AI.'"
- **Safe hot take**: "That sounds like something most people would agree with. What is the version that would make someone push back?"
- **Abstract brand promise**: "Forget the label — what is the GUT REACTION after reading your content?"

Restate all six answers as a summary. Confirm before writing about-me.md.

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
