---
name: skill-creator
description: >
  Build a new Claude skill from scratch. Triggers on "build a skill for X",
  "create a skill", or when a manual repetitive process should be formalized
  into a reusable skill.
---

# Skill Creator

You are a conversational agent guiding a human through 4 phases of skill creation. Walk the human through each phase, present findings, and only proceed when explicitly approved. Each phase ends with a **HUMAN GATE**.

## When to Use

- Creating a new Claude skill from scratch
- Someone says "build a skill", "create a skill", "new skill for X"
- Automating a recurring manual workflow as a reusable skill
- Scaffolding a SKILL.md for a new capability

---

## Phase 0: Interview

**Purpose:** Understand what the user wants to build.

**Steps:**

1. Ask: "What problem does this skill solve? What triggers it?"
2. Ask: "What tools, APIs, or data sources does it need?"
3. Ask: "Will it accept arguments? (e.g., `/skill-name <arg>`)"
4. Ask: "How complex is this? Simple (single file SKILL.md), medium (SKILL.md + references), or advanced (SKILL.md + scripts + references)?"

**HUMAN GATE:** Present a summary table of all gathered context. Ask:
- "Does this summary capture what you want to build?"
- "Anything missing or wrong?"

---

## Phase 1: Skill Identity

**Purpose:** Lock in name, description, and frontmatter.

**Steps:**

1. Generate a kebab-case name (lowercase, hyphens, 1-64 chars).
2. Draft a trigger-focused description (verb-first, 20-40 words). The description should explain both WHAT the skill does and WHEN it should activate.
3. Draft a "When to Use" bullet list (4-7 trigger scenarios).

**HUMAN GATE:** Present the frontmatter + When to Use. Ask:
- "Does this name match how you'd invoke it? (`/skill-name`)"
- "Is the description clear enough for auto-activation?"
- "Any trigger scenarios missing?"

---

## Phase 2: Folder Structure

**Purpose:** Create the directory layout.

**Steps:**

1. Based on complexity from Phase 0, propose a folder structure:
   - **Simple:** `skills/{name}/SKILL.md` only
   - **Medium:** `skills/{name}/SKILL.md` + `skills/{name}/references/` for YAML data files
   - **Advanced:** Above + `skills/{name}/scripts/` for executable scripts
2. Present the exact folder tree with file purposes.
3. After approval, create all directories.

**HUMAN GATE:** Present the proposed folder tree. Ask:
- "Does this structure look right?"
- "Any folders to add or remove?"

---

## Phase 3: SKILL.md Generation

**Purpose:** Write the core skill file using this template:

```yaml
---
name: [skill-name]
description: >
  [One paragraph describing what this skill does and when to trigger it.]
---

# [Skill Name]

## Auto-start on load
[Instructions for immediate action when triggered]

## Step 1. [First action]
[Instructions]

## Step 2. [Second action]
[Instructions]

## Rules
- [Rule 1]
- [Rule 2]
```

**Steps:**

1. Fill in the template based on everything gathered in Phases 0-1.
2. For guided workflows: add numbered phases with HUMAN GATES.
3. For automation skills: add clear step-by-step instructions.
4. Keep SKILL.md lean -- reference external files by path, don't inline large data.
5. If the skill needs reference YAML files (taxonomies, schemas, rubrics), draft those too.

**HUMAN GATE:** Present the generated SKILL.md. Ask:
- "Does the flow make sense?"
- "Are the instructions specific enough?"
- "Anything to add or change?"

## Rules

- Each phase requires explicit user approval before proceeding.
- Names must be kebab-case, 1-64 characters.
- Descriptions must be trigger-focused (verb-first, explain WHAT + WHEN).
- Keep SKILL.md under 200 lines. Offload data to references/ YAML files.
- Never generate scripts without the user requesting them.
