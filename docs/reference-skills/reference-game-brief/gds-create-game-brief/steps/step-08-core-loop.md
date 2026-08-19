> AGDA file-first override: write or update `preproduction/design.md` immediately when the player's answer gives enough information. Do not wait for per-section CONTINUE, do not present REFINE/CONTINUE menus inside this stage, and do not post full drafts into chat unless requested. CONTINUE is only for the stage boundary after the complete `preproduction/design.md` is ready.

---
name: 'step-08-core-loop'
description: 'Guide core loop design after content and production'

# Path Definitions
workflow_path: '{installed_path}'

# File References
thisStepFile: './step-08-core-loop.md'
nextStepFile: './step-09-mda-motivation.md'
workflowFile: '{workflow_path}/workflow.md'
outputFile: 'preproduction/design.md'
---

# Step 8: Core Loop Design

**Progress: Step 8 of 12** - Next: MDA and Player Motivation

## STEP GOAL:

Define the moment-to-moment, short-term, session, and long-term loops as a guided design conversation.

## MANDATORY EXECUTION RULES:

- NEVER generate content without user input.
- Act as a facilitator, not a silent generator.
- Ask focused questions only when needed, then save the section directly to preproduction/design.md and continue.
- Challenge loops that are passive, vague, or depend on broad content scale instead of repeatable play.

## Sequence of Instructions

### 1. Moment-to-Moment Loop

Ask:

"What is the player physically or mentally doing every 30 seconds? Describe the repeated action, the immediate feedback, and why it should feel good even before progression rewards exist."

Capture:

- Core action
- Feedback
- Reward
- New choice
- What makes it intrinsically satisfying

### 2. Short-Term Loop

Ask:

"What structures several moments into a 5-15 minute cycle? Where does the 'one more turn', 'one more run', or 'one more attempt' pull come from?"

Capture:

- Objective
- Pressure or constraint
- Resolution
- Reward or learning
- Next decision

### 3. Session Loop

Ask:

"What does one complete play session look like? Where can the player stop cleanly, and what makes them want to return?"

Capture:

- Session goal
- Main challenge
- Session reward
- Stopping point
- Return hook

### 4. Long-Term Progression

Ask:

"How does the player grow across days or weeks: power, knowledge, options, mastery, story, world state, or something else?"

Capture:

- Progression vector
- Unlocks or mastery path
- Long-term goal
- End condition or evergreen motivation

### 5. Generate Core Loop Section

Prepare:

```markdown
## Core Loop Design

| Loop Level | Player Action | Feedback / Reward | Design Risk |
|---|---|---|---|
| Moment-to-moment | {{moment_action}} | {{moment_feedback}} | {{moment_risk}} |
| Short-term | {{short_action}} | {{short_reward}} | {{short_risk}} |
| Session | {{session_action}} | {{session_reward}} | {{session_risk}} |
| Long-term progression | {{progression_action}} | {{progression_reward}} | {{progression_risk}} |

- **Retention hooks:** {{retention_hooks}}
- **Core loop validation question:** {{core_loop_validation_question}}
```

### 6. Present Menu

Edit/refinement: apply corrections directly to `preproduction/design.md`.
Stage boundary: use CONTINUE only after the complete game-conception stage is ready.

### 7. Handle Selection

If the player refines, ask only the targeted follow-up needed and edit `preproduction/design.md`.

Do not use CONTINUE inside the stage; proceed by updating `preproduction/design.md` and asking the next focused question.

- Append the final section to `{outputFile}`
- Replace the existing Core Loop Design section in `{outputFile}` if it already exists.
- Update frontmatter: `stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8]`
- Load `{nextStepFile}`

