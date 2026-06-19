# Exercise 1: LinkedIn Content

Build your personal voice profile and write your first AI-powered LinkedIn post.

## Prerequisites

- [ ] Claude Cowork installed and open
- [ ] Plugin 01 installed: Settings → Extensions → Add from folder → `.claude/plugins/01-linkedin-content/`
- [ ] 3 to 5 writing samples ready (LinkedIn posts, blog posts, emails, or any published writing)
- [ ] Optional: your website or blog URL

## What you will build

1. **about-me.md** — Who you are: name, role, audience, topics, point of view, brand promise
2. **voice.md** — How you write: tone, rhythm, hooks, signature phrases, what your voice never does
3. **A LinkedIn post** — Written by Claude in your voice, about a topic you choose

## Steps

### Step 1: Start the Voice Builder

Open a new conversation in Claude Cowork. The voice-builder skill auto-starts the moment the plugin is active.

Claude will ask you to paste your website URL or skip to the interview.

- **If you have a website**: paste the URL. Claude will analyze your brand, tone, and content topics.
- **If you don't**: type "skip" and go straight to the interview.

### Step 2: Answer the interview (2 min)

Claude will ask 6 questions in 2 rounds:

**Round 1** (click to answer):
1. What is your name and what do you do?
2. Who are you writing for?
3. What are the 3-5 topics you want to be known for?
4. What is your point of view on your industry?

**Round 2**:
5. What is the one thing you want people to think when they see your name?
6. What topics do you refuse to write about?

These are multiple-choice with an "Other" option. Pick what fits or type your own answer.

### Step 3: Paste your writing samples (5 min)

Claude will ask for 3 to 5 pieces of writing. Paste them one at a time or all at once.

**What works well:**
- LinkedIn posts you are proud of
- Blog posts or newsletter issues
- Emails where your personality comes through
- Writing from someone whose voice you admire (Claude will note it's a reference, not your voice)

**If you don't have samples ready:** Type "use samples" and Claude will load a starter set.

### Step 4: Review your voice profile

Claude will create two files:

- **about-me.md**: Check that your name, role, audience, and topics are correct. Edit anything that feels off.
- **voice.md**: Read through the tone, hook patterns, and "what this voice never does" section. These are based on your actual writing patterns.

### Step 5: Write a post

Say "write a post" to trigger the post-writer skill.

Claude will ask:
1. What topic? (paste ideas, type a topic, or let Claude suggest)
2. Which angle and framework? (Claude presents options based on research)

Then Claude writes a draft in your voice. Output appears in a code block you can copy directly to LinkedIn.

### Step 6: Iterate

Read the draft. Tell Claude what to change ("make the hook sharper", "add a concrete example", "shorter paragraphs"). Maximum 3 revision rounds, then "ship it" to save.

## Verification

- [ ] about-me.md exists in your project with your name and topics
- [ ] voice.md exists with tone, hooks, and absence patterns from your samples
- [ ] You have at least one LinkedIn post draft in a code block
- [ ] The post sounds like you, not like generic AI

## Take-home

Your voice profile persists in this project. Every future conversation in this project will reference about-me.md and voice.md automatically. Come back anytime and say "write a post" to generate more content in your voice.

**Bonus**: Check out the Content Toolkit (post-formatter, hook-generator, content-matrix) in Plugin 03 for more content creation tools.
