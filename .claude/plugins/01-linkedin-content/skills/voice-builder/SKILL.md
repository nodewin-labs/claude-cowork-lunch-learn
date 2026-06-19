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
3. **Render the Brand Analysis Card** — generate a self-contained HTML artifact using the template below. Fill ALL placeholders with actual extracted data. Do NOT show a text summary first — go straight to the visual card.
4. After the card renders, ask: "Does this capture your brand? Anything to adjust?"
5. Store the confirmed results for use in about-me.md and for building dynamic interview options in Step 2.

If the user types "skip": proceed directly to Step 2.

### Brand Analysis Card (HTML artifact template)

After extracting website data, generate this HTML artifact. Replace every `{{placeholder}}` with actual data. Adjust the number of sub-promise pills and vocabulary tags to match what you found. The card must work for ANY brand — no hardcoded company names, colors, or logos.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif; background: #0a0a0a; color: #e5e5e5; padding: 32px; min-height: 100vh; display: flex; justify-content: center; align-items: flex-start; }
  .card { max-width: 640px; width: 100%; background: #141414; border: 1px solid #262626; border-radius: 16px; overflow: hidden; }
  .card-header { padding: 28px 32px 20px; border-bottom: 1px solid #262626; }
  .card-header .label { font-size: 11px; text-transform: uppercase; letter-spacing: 1.5px; color: #737373; margin-bottom: 8px; }
  .card-header h1 { font-size: 22px; font-weight: 600; color: #fafafa; line-height: 1.3; }
  .card-header .url { font-size: 13px; color: #525252; margin-top: 6px; }
  .section { padding: 20px 32px; border-bottom: 1px solid #1a1a1a; }
  .section:last-child { border-bottom: none; }
  .section-label { font-size: 11px; text-transform: uppercase; letter-spacing: 1.5px; color: #737373; margin-bottom: 12px; }
  .promise { font-size: 17px; color: #fafafa; line-height: 1.5; font-weight: 500; }
  .pills { display: flex; flex-wrap: wrap; gap: 8px; }
  .pill { background: #1a1a1a; border: 1px solid #333; border-radius: 20px; padding: 6px 14px; font-size: 13px; color: #d4d4d4; }
  .tone-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
  .tone-item { background: #1a1a1a; border-radius: 10px; padding: 14px 16px; }
  .tone-item .tone-label { font-size: 11px; text-transform: uppercase; letter-spacing: 1px; color: #737373; margin-bottom: 4px; }
  .tone-item .tone-value { font-size: 14px; color: #e5e5e5; }
  .vocab-tags { display: flex; flex-wrap: wrap; gap: 6px; }
  .vocab-tag { background: #1c1c1c; border: 1px solid #2a2a2a; border-radius: 6px; padding: 4px 10px; font-size: 12px; color: #a3a3a3; font-family: 'SF Mono', 'Fira Code', monospace; }
  .personality { font-size: 14px; color: #d4d4d4; line-height: 1.6; font-style: italic; }
</style>
</head>
<body>
<div class="card">
  <div class="card-header">
    <div class="label">Brand Analysis</div>
    <h1>{{brand_name_or_page_title}}</h1>
    <div class="url">{{url}}</div>
  </div>

  <div class="section">
    <div class="section-label">Brand Promise</div>
    <div class="promise">{{brand_promise_one_sentence}}</div>
  </div>

  <div class="section">
    <div class="section-label">Sub-Promises</div>
    <div class="pills">
      <span class="pill">{{sub_promise_1}}</span>
      <span class="pill">{{sub_promise_2}}</span>
      <span class="pill">{{sub_promise_3}}</span>
      <!-- add more pills if more sub-promises were found -->
    </div>
  </div>

  <div class="section">
    <div class="section-label">Tone</div>
    <div class="tone-grid">
      <div class="tone-item">
        <div class="tone-label">Voice</div>
        <div class="tone-value">{{tone_voice, e.g. "Confident, direct"}}</div>
      </div>
      <div class="tone-item">
        <div class="tone-label">Register</div>
        <div class="tone-value">{{tone_register, e.g. "Practitioner, no fluff"}}</div>
      </div>
      <div class="tone-item">
        <div class="tone-label">Energy</div>
        <div class="tone-value">{{tone_energy, e.g. "Action-oriented, builder language"}}</div>
      </div>
      <div class="tone-item">
        <div class="tone-label">POV</div>
        <div class="tone-value">{{tone_pov, e.g. "First person plural, inclusive"}}</div>
      </div>
    </div>
  </div>

  <div class="section">
    <div class="section-label">Vocabulary</div>
    <div class="vocab-tags">
      <span class="vocab-tag">{{vocab_1}}</span>
      <span class="vocab-tag">{{vocab_2}}</span>
      <span class="vocab-tag">{{vocab_3}}</span>
      <span class="vocab-tag">{{vocab_4}}</span>
      <span class="vocab-tag">{{vocab_5}}</span>
      <span class="vocab-tag">{{vocab_6}}</span>
      <!-- add more tags as found -->
    </div>
  </div>

  <div class="section">
    <div class="section-label">Brand Personality</div>
    <div class="personality">{{personality_summary_one_or_two_sentences}}</div>
  </div>
</div>
</body>
</html>
```

**Rules for the card:**
- Replace ALL `{{placeholders}}` with real data from the website analysis
- Add or remove pills, tone items, and vocab tags to match what was actually found — do not leave placeholders or show empty items
- Do NOT hardcode any company name, color, or logo — the dark theme works for any brand
- If a section has no data (e.g. no vocabulary patterns found), omit that section entirely

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

Read every sample. Extract patterns across ALL samples in four categories:

### 5a. Positive patterns (what this voice DOES)

**Voice signals**: hook style, POV, tone, signature phrases, closing style

**Sentence metrics** (calculate precisely, not approximately):
- Count total sentences across all samples
- Calculate average sentence length in words
- Find the range (shortest and longest sentence lengths)
- Calculate average paragraph length in sentences
- Note the pacing pattern (do sentences alternate short/long? build in length? stay consistent?)

**Structural signals**: length range, lists vs prose, transitions

**Topic signals**: recurring subjects, apparent audience

### 5b. Absence patterns (what this voice NEVER does)

Scan all samples for what is consistently absent:
- Words and punctuation never used (e.g. em dashes in 0 of 5 samples)
- Hook types never deployed (e.g. never opens with a rhetorical question)
- Tones never hit (e.g. never motivational, never apologetic)
- Structural moves never made (e.g. never uses numbered lists, never ends with a question)

### 5c. AI pattern scan

Cross-reference the samples against common AI writing patterns. For each pattern below, check: does this voice use it (found in samples), avoid it (absent from all samples), or is it ambiguous?

**Phrases to scan for:**
- "Here's the thing..." / "Here's what nobody tells you..."
- "Let me be honest..." / "Let's be real..."
- "Not X, but Y" constructions ("Not a tool, but a mindset")
- "The truth is..." / "The reality is..."
- "Game-changer" / "Unlock" / "Leverage" / "Navigate" / "Elevate"
- "Deep dive" / "Double down" / "Move the needle"
- "In today's [fast-paced/ever-changing] world..."
- "If you're not doing X, you're falling behind"
- Stacked rhetorical questions as hooks
- Motivational closing ("You've got this!" / "The time to start is now")
- Em dashes used for dramatic pauses
- Parenthetical asides (brackets for commentary)
- Emoji-heavy formatting
- "I" as the first word of the post
- Listicle padding ("Here are 7 things...")

**For each pattern found in the samples**: note it as part of the voice (keep it).
**For each pattern absent from all samples**: flag it as a banned pattern.
**For patterns the user's samples don't clearly resolve**: ask the user via AskUserQuestion — present the ambiguous patterns and ask which they want to ban:

```json
[
  {
    "question": "I found some writing patterns in your samples that could go either way. Which of these do you want to AVOID in your content?",
    "header": "Anti-patterns",
    "multiSelect": true,
    "options": [
      {"label": "[pattern 1]", "description": "[example of how it looks + why it might feel AI-generated]"},
      {"label": "[pattern 2]", "description": "[example]"},
      {"label": "[pattern 3]", "description": "[example]"}
    ]
  }
]
```

Only ask about genuinely ambiguous patterns. If the samples clearly use or clearly avoid a pattern, do not ask — just record it.

## Step 6. Write voice.md

Create voice.md in the project root:

```
# Voice Profile

## Who I sound like
[2-3 sentences describing the overall voice]

## Tone
[3-5 attributes the voice hits, plus 1-2 tones it never hits]

## Sentence rhythm
- Average sentence length: [X words — calculated from samples]
- Range: [shortest avg to longest avg across samples, e.g. "8-22 words"]
- Paragraph length: [X sentences per paragraph on average]
- Pacing pattern: [e.g. "short-short-long", "consistent medium", "opens short then builds"]
- Avoidance: [e.g. "never exceeds 30 words in a sentence", "no single-word paragraphs"]

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

## Banned phrases and patterns
[Concrete list of phrases and structural patterns this voice must NEVER use. Each item includes the pattern and why it is banned. Sources: absence from samples + AI pattern scan + user confirmation.]

Examples of what this section looks like when filled:
- Never use em dashes for dramatic pauses (0 of 5 samples)
- Never open with "Here's the thing..." or "Here's what nobody tells you..." (AI-ism, absent from samples)
- Never use "game-changer", "unlock", "leverage", "navigate", "elevate" (corporate AI vocabulary)
- Never use "Not X, but Y" constructions (absent from all samples, common AI pattern)
- Never use stacked rhetorical questions as hooks (user confirmed ban)
- Never end with motivational closers like "You've got this!" (tone mismatch)
- Never start a post with "I" as the first word (absent from samples)
- Never use "In today's [adjective] world..." (AI-ism filler)

Only include patterns that are actually banned based on sample analysis + user input. Do not copy this example list verbatim.

## What this voice never does
[3-5 specific behavioural patterns from gaps in the samples — broader than individual phrases. E.g. "never hedges a strong opinion", "never addresses the reader as 'friend'", "never uses more than one emoji per post"]
```

Fill every section from actual data. No generic filler. Keep under 600 words (increased from 500 to accommodate banned patterns).

## Step 7. Render Voice Profile Card and hand off

After writing both files, generate a final HTML artifact — the Voice Profile Card. This is the visual summary of everything: identity + voice in one shareable card. Use the template below, filling ALL placeholders from about-me.md and voice.md.

Then say:

> Your voice profile is built. Two files are in your project (about-me.md and voice.md) and here is your visual profile card.
>
> Say "write a post" to draft a LinkedIn post in your voice.

### Voice Profile Card (HTML artifact template)

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif; background: #0a0a0a; color: #e5e5e5; padding: 32px; min-height: 100vh; display: flex; justify-content: center; align-items: flex-start; }
  .card { max-width: 640px; width: 100%; background: #141414; border: 1px solid #262626; border-radius: 16px; overflow: hidden; }
  .card-header { padding: 28px 32px 20px; border-bottom: 1px solid #262626; background: linear-gradient(135deg, #141414 0%, #1a1a2e 100%); }
  .card-header .label { font-size: 11px; text-transform: uppercase; letter-spacing: 1.5px; color: #737373; margin-bottom: 8px; }
  .card-header h1 { font-size: 24px; font-weight: 600; color: #fafafa; line-height: 1.3; }
  .card-header .subtitle { font-size: 14px; color: #a3a3a3; margin-top: 6px; }
  .section { padding: 20px 32px; border-bottom: 1px solid #1a1a1a; }
  .section:last-child { border-bottom: none; }
  .section-label { font-size: 11px; text-transform: uppercase; letter-spacing: 1.5px; color: #737373; margin-bottom: 12px; }
  .pov { font-size: 16px; color: #fafafa; line-height: 1.5; font-weight: 500; font-style: italic; border-left: 3px solid #444; padding-left: 16px; }
  .pills { display: flex; flex-wrap: wrap; gap: 8px; }
  .pill { background: #1a1a1a; border: 1px solid #333; border-radius: 20px; padding: 6px 14px; font-size: 13px; color: #d4d4d4; }
  .pill.accent { border-color: #4a4a6a; background: #1a1a2e; }
  .voice-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
  .voice-item { background: #1a1a1a; border-radius: 10px; padding: 14px 16px; }
  .voice-item .v-label { font-size: 11px; text-transform: uppercase; letter-spacing: 1px; color: #737373; margin-bottom: 4px; }
  .voice-item .v-value { font-size: 14px; color: #e5e5e5; }
  .hooks { list-style: none; }
  .hooks li { padding: 8px 0; border-bottom: 1px solid #1a1a1a; font-size: 14px; color: #d4d4d4; }
  .hooks li:last-child { border-bottom: none; }
  .hooks .hook-type { color: #737373; font-size: 12px; text-transform: uppercase; letter-spacing: 0.5px; }
  .hooks .hook-example { margin-top: 4px; color: #a3a3a3; font-style: italic; font-size: 13px; }
  .never-list { list-style: none; }
  .never-list li { padding: 6px 0; font-size: 14px; color: #d4d4d4; }
  .never-list li::before { content: "✕ "; color: #666; }
  .banned-list { list-style: none; }
  .banned-list li { padding: 5px 0; font-size: 13px; color: #d4d4d4; display: flex; align-items: baseline; gap: 8px; }
  .banned-list .phrase { background: #2a1a1a; border: 1px solid #4a2a2a; border-radius: 4px; padding: 2px 8px; font-family: 'SF Mono', 'Fira Code', monospace; font-size: 12px; color: #e5a3a3; white-space: nowrap; }
  .banned-list .reason { color: #737373; font-size: 12px; }
  .summary { font-size: 14px; color: #d4d4d4; line-height: 1.6; }
</style>
</head>
<body>
<div class="card">
  <div class="card-header">
    <div class="label">Voice Profile</div>
    <h1>{{name}}</h1>
    <div class="subtitle">{{role}} · Writing for {{audience_short}}</div>
  </div>

  <div class="section">
    <div class="section-label">Point of View</div>
    <div class="pov">{{point_of_view_statement}}</div>
  </div>

  <div class="section">
    <div class="section-label">Topic Pillars</div>
    <div class="pills">
      <span class="pill accent">{{topic_1}}</span>
      <span class="pill accent">{{topic_2}}</span>
      <span class="pill accent">{{topic_3}}</span>
      <!-- add more as needed -->
    </div>
  </div>

  <div class="section">
    <div class="section-label">How This Voice Sounds</div>
    <div class="voice-grid">
      <div class="voice-item">
        <div class="v-label">Tone</div>
        <div class="v-value">{{tone_attributes}}</div>
      </div>
      <div class="voice-item">
        <div class="v-label">Rhythm</div>
        <div class="v-value">{{sentence_rhythm_summary}}</div>
      </div>
      <div class="voice-item">
        <div class="v-label">POV</div>
        <div class="v-value">{{writing_pov}}</div>
      </div>
      <div class="voice-item">
        <div class="v-label">Length</div>
        <div class="v-value">{{post_length_range}}</div>
      </div>
    </div>
  </div>

  <div class="section">
    <div class="section-label">Hook Patterns</div>
    <ul class="hooks">
      <li>
        <div class="hook-type">{{hook_type_1}}</div>
        <div class="hook-example">"{{hook_example_1}}"</div>
      </li>
      <li>
        <div class="hook-type">{{hook_type_2}}</div>
        <div class="hook-example">"{{hook_example_2}}"</div>
      </li>
      <li>
        <div class="hook-type">{{hook_type_3}}</div>
        <div class="hook-example">"{{hook_example_3}}"</div>
      </li>
    </ul>
  </div>

  <div class="section">
    <div class="section-label">Banned Phrases & Patterns</div>
    <ul class="banned-list">
      <li><span class="phrase">{{banned_phrase_1}}</span> <span class="reason">{{reason_1}}</span></li>
      <li><span class="phrase">{{banned_phrase_2}}</span> <span class="reason">{{reason_2}}</span></li>
      <li><span class="phrase">{{banned_phrase_3}}</span> <span class="reason">{{reason_3}}</span></li>
      <!-- add more as found — typically 5-10 banned patterns -->
    </ul>
  </div>

  <div class="section">
    <div class="section-label">What This Voice Never Does</div>
    <ul class="never-list">
      <li>{{never_1}}</li>
      <li>{{never_2}}</li>
      <li>{{never_3}}</li>
      <!-- add more as found -->
    </ul>
  </div>

  <div class="section">
    <div class="section-label">Brand Promise</div>
    <div class="summary">{{brand_promise_personal}}</div>
  </div>
</div>
</body>
</html>
```

**Rules for the Voice Profile Card:**
- Replace ALL `{{placeholders}}` with real data from about-me.md and voice.md
- Add or remove hook items, never-list items, topic pills to match actual data
- Do NOT hardcode any name, company, or color — the dark theme is universal
- If a section has no data, omit it
- This card is the final "wow" deliverable — make it accurate

## Rules

- Auto-start on load. No summary, no preamble.
- Output files in code blocks for easy copy-paste.
- Work from what is in the samples. Do not invent patterns.
- Minimum 3 samples for pattern detection.
- If samples contradict, note the contradiction rather than smoothing it.
- Keep about-me.md under 300 words, voice.md under 500 words.
- British English unless samples are clearly American.
- Never use em dashes in any output.
