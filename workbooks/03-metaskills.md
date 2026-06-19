# Exercise 3: Metaskills

Build a custom skill from your most repetitive workflow. Claude interviews you, understands the process, and generates a SKILL.md you can use forever.

## Prerequisites

- [ ] Claude Cowork installed and open
- [ ] Plugin 03 installed: Settings → Extensions → Add from folder → `.claude/plugins/03-metaskills/`
- [ ] Think of one task you do every week that takes too long or is tedious

## What you will build

1. A custom **SKILL.md** file tailored to YOUR specific workflow
2. A working skill you can trigger in Claude Cowork from now on

## What is in this plugin

This plugin includes 6 metaskills:

| Skill | What it does |
|-------|-------------|
| **interview** | Structured questioning to reach 95% confidence about what you actually want |
| **problem-statement** | Frame a problem clearly before jumping to solutions |
| **problem-solution** | Explore and evaluate solution options for a framed problem |
| **compare-options** | Structured pro/con analysis with a clear recommendation |
| **skill-creator** | Generate a custom SKILL.md from your workflow description |
| **skill-audit** | Review and improve an existing SKILL.md |

## Steps

### Step 1: Identify your workflow

Before starting, think about a task that:
- You do every week (or more often)
- Takes at least 15 minutes each time
- Follows roughly the same steps
- Requires gathering info from multiple places

**Examples:**
- Writing a weekly client update email
- Preparing a sales call summary
- Creating a social media content calendar
- Processing expense reports
- Writing meeting notes and action items
- Generating a weekly team status report

Write down the task name and a one-sentence description.

### Step 2: Let Claude interview you

Say "interview me about my workflow" or just describe your task. Claude will use the interview skill to understand:

- What triggers the task?
- What inputs do you need?
- What steps do you follow?
- What does the output look like?
- What tools or systems are involved?
- What are the annoying parts?

Claude will keep asking until it reaches 95% confidence. It will challenge your assumptions and restate what it understood for confirmation.

### Step 3: Generate your skill

Once the interview is complete, say "create a skill for this" or Claude will offer to generate one.

The skill-creator will:
1. Define the skill identity (name, trigger phrases)
2. Create the folder structure
3. Write the SKILL.md with:
   - Auto-start instructions
   - Step-by-step workflow
   - AskUserQuestion interactions
   - Rules and constraints
   - Output format

### Step 4: Test your skill

Claude will show you the generated SKILL.md. Read through it and check:
- Does the trigger description match when you would use this?
- Do the steps match your actual workflow?
- Are the inputs and outputs correct?

Then test it: trigger the skill by saying its trigger phrase. Walk through one real example.

### Step 5: Iterate

If something is off, tell Claude:
- "Step 3 should ask for [X] before [Y]"
- "Add a rule that [constraint]"
- "The output should include [section]"

Claude will update the SKILL.md. You can also run `/skill-audit` to get a structured review.

## Verification

- [ ] You have a SKILL.md file for your workflow
- [ ] The skill has a clear name and trigger description
- [ ] The steps match your actual process
- [ ] You tested the skill with a real example
- [ ] The output is useful and saves you time

## Take-home

### Using your skill going forward

Your custom SKILL.md lives in your Claude Cowork project. Every time you open this project, Claude knows about your skill. Trigger it whenever you need it.

### Building more skills

You can run the skill-creator again for any workflow. Over time, build a library of skills that automate your repetitive tasks. Each skill is a plain markdown file — easy to share with colleagues.

### Improving existing skills

Run `/skill-audit` on any SKILL.md to get structured feedback on how to make it better. Common improvements:
- Adding AskUserQuestion interactions instead of free-text prompts
- Adding verification checkpoints
- Tightening the rules section
- Adding edge case handling

### Thinking toolkit

The other metaskills in this plugin are useful beyond skill creation:
- **/interview** — Use before any important conversation to clarify what you actually want
- **/problem-statement** — Use when stuck to frame the real problem
- **/compare-options** — Use when deciding between alternatives
