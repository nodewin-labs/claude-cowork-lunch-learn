---
name: post-writer
description: >
  Write LinkedIn posts that match your voice profile (about-me.md and voice.md). Use whenever you say "write a post", "draft a post", "LinkedIn post", "post about [topic]", or paste a context dump to turn into a post. Always references voice files before writing. Always outputs the final post in a code block.
---

# Post Writer

## CRITICAL: Auto-start on load

The moment this skill triggers, go straight to Step 1. No summary, no explanation. Jump to input gathering immediately.

## Step 1. Gather inputs

Check the project for about-me.md and voice.md. Read both. If either is missing, tell the user to run the Voice Builder skill first ("say build my voice"), then stop.

If both files exist, call AskUserQuestion:

```json
[
  {
    "question": "What topic do you want to post about?",
    "header": "Topic",
    "multiSelect": false,
    "options": [
      {"label": "Paste a context dump", "description": "I have notes, transcripts, or raw ideas to turn into a post"},
      {"label": "I have a topic in mind", "description": "I will type the topic after this"},
      {"label": "Suggest topics for me", "description": "Based on my voice system, suggest 5 topics I should post about"}
    ]
  },
  {
    "question": "Do you have any reference posts you want me to use as structural inspiration?",
    "header": "References",
    "multiSelect": false,
    "options": [
      {"label": "No references", "description": "Write from scratch using my voice files only"},
      {"label": "I will paste examples", "description": "I have posts from other creators I want you to study first"},
      {"label": "Use my training posts", "description": "Reference the posts I used in the Voice Builder"}
    ]
  }
]
```

Based on answers:
- "Paste a context dump": wait for paste, extract core idea, proceed to Step 2
- "I have a topic in mind": wait for topic, proceed to Step 2
- "Suggest topics for me": read about-me.md topic pillars, suggest 5 topics with angles, let user pick
- "I will paste examples": wait for posts, note patterns, proceed
- "Use my training posts": reference posts already in the project

## Step 2. Research and plan

Before writing, research the topic:
- Data points or statistics that support the angle
- Contrarian takes or surprising facts
- Real examples or case studies
- Common misconceptions to challenge

Then present a post plan via AskUserQuestion:

```json
[
  {
    "question": "Which angle works best for this post?",
    "header": "Angle",
    "multiSelect": false,
    "options": [
      {"label": "[Angle 1 name]", "description": "[One sentence describing the angle and hook]"},
      {"label": "[Angle 2 name]", "description": "[One sentence describing the angle and hook]"},
      {"label": "[Angle 3 name]", "description": "[One sentence describing the angle and hook]"}
    ]
  },
  {
    "question": "Which framework do you want?",
    "header": "Framework",
    "multiSelect": false,
    "options": [
      {"label": "PAS", "description": "Problem, Agitate, Solution"},
      {"label": "How-to list", "description": "Numbered steps or tips"},
      {"label": "Story to lesson", "description": "Personal story with a takeaway"},
      {"label": "Contrarian take", "description": "Challenge a common belief"}
    ]
  }
]
```

Fill in actual angle options based on topic research.

## Step 3. Write the draft

### 3a. Show the writing brief

Before writing a single word, read voice.md and about-me.md and present the user with a visible brief — the rules this post will follow. Extract every relevant constraint and show it:

> **Writing brief for this post:**
>
> | Constraint | Value |
> |-----------|-------|
> | **Tone** | [from voice.md — e.g. "Confident, direct, no fluff"] |
> | **POV** | [from voice.md — e.g. "First person singular"] |
> | **Avg sentence length** | [from voice.md — e.g. "14 words (range: 8-22)"] |
> | **Paragraph length** | [from voice.md — e.g. "2-3 sentences"] |
> | **Post length** | [150-300 words unless user requested otherwise] |
> | **Hook style** | [the hook pattern chosen in Step 2] |
> | **Closing style** | [from voice.md — e.g. "Direct CTA, no motivational fluff"] |
> | **Format** | [from voice.md — e.g. "Prose over lists, no emoji"] |
>
> **Banned patterns** (zero tolerance):
> - [banned phrase 1 from voice.md]
> - [banned phrase 2]
> - [banned phrase 3]
> - [...all banned patterns from voice.md]
>
> **This voice never:**
> - [never-does 1 from voice.md]
> - [never-does 2]
> - [...]

Fill every row from actual voice.md data. Do not show empty or placeholder rows. If voice.md does not have data for a constraint, omit that row.

Wait for the user to confirm or adjust before writing. If they say "looks good" or similar, proceed. If they want to override a constraint for this specific post (e.g. "make it longer this time"), note the override.

### 3b. Write the post

Now write, following every constraint from the brief:
- Match the sentence length range — if average is 14 words, keep most sentences between 10-18 words
- Match the paragraph rhythm and pacing pattern
- Check every sentence against the banned patterns list — if a sentence contains a banned phrase, rewrite it
- Use the hook pattern from the brief
- End with the closing style from the brief
- Apply any user overrides from 3a

Output inside a plain code block:

```
[The full post with all line breaks and formatting as it should appear on LinkedIn]
```

After the code block, add 2-3 sentences on why you chose this hook and structure, referencing specific patterns from voice.md.

## Step 4. Iterate

> How does this feel? Tell me what to change, or say "ship it" to save the final version.

If feedback: revise and output new code block. Maximum 3 revision rounds.

If "ship it": save as a markdown file in the project.

> Post saved. You can come back anytime and say "write a post" to create more content in your voice.

## Rules

- Always read about-me.md and voice.md before writing.
- Always output posts in a plain code block.
- Never use any phrase listed in voice.md's "Banned phrases and patterns" section. Zero tolerance.
- Match the sentence length metrics from voice.md. If average is 14 words, do not write 25-word sentences.
- British English unless voice.md says otherwise.
- Do not add hashtags unless voice.md explicitly uses them.
- Do not add engagement bait CTAs unless they appear in voice.md.
- Keep posts between 150 and 300 words unless requested otherwise.
- Plan before writing. Never skip Step 2.
