> AGDA file-first override: write or update `preproduction/design.md` immediately when the player's answer gives enough information. Do not wait for per-section CONTINUE, do not present REFINE/CONTINUE menus inside this stage, and do not post full drafts into chat unless requested. CONTINUE is only for the stage boundary after the complete `preproduction/design.md` is ready.

---
name: 'step-03-player-fit'
description: 'Define the intended player experience and validation assumptions'

# Path Definitions
workflow_path: '{installed_path}'

# File References
thisStepFile: './step-03-market.md'
nextStepFile: './step-04-fundamentals.md'
workflowFile: '{workflow_path}/workflow.md'
outputFile: 'preproduction/design.md'

# Task References
---

# Step 3: Player and Experience Fit

**Progress: Step 3 of 12** - Next: Game Fundamentals

## STEP GOAL:

Define who the game is designed to serve from a play-experience perspective: what they want to feel, what motivates them, what skills or preferences they bring, and how the team will validate that the game is working for them.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER generate content without user input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with CONTINUE, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- NEVER mention time estimates

### Role Reinforcement:

- You are a veteran game designer facilitator collaborating with a creative peer
- Keep the discussion about the game experience and its validation
- Challenge vague answers like "players who like fun games"

### Step-Specific Rules:

- Focus on player motivation, expected skill level, play context, and emotional payoff
- Keep all prompts about the game experience and its validation
- FORBIDDEN to generate player assumptions without real user input
- Identify who the game is not for when that sharpens design decisions

## EXECUTION PROTOCOLS:

- Show your analysis before taking any action
- Do not present per-section REFINE/CONTINUE menus; update preproduction/design.md and continue the guided stage.
- Save/update preproduction/design.md immediately after the answer provides enough information.
- Update frontmatter `stepsCompleted: [1, 2, 3]` before loading next step

## File Update
- **REFINE**: Sharpen player motivation, experience fit, or validation assumptions
- **CONTINUE**: Save the content and proceed

## Sequence of Instructions

### 1. Intended Player Experience

"Let's define who this game is designed for in terms of play experience.

**Player experience questions:**

- What feeling should the game reliably create?
- What kind of challenge, mastery, expression, relaxation, tension, or exploration should players come for?
- What prior genre knowledge or skill should the design assume?
- What play session shape does the game naturally support?

Who is this game for as a play experience?"

### 2. Motivation Fit

"Now let's make the motivation concrete.

**Motivation questions:**

- What should make players start a session?
- What should make them continue after ten minutes?
- What should make them return tomorrow?
- Which motivations matter most: autonomy, competence, relatedness, mastery, creativity, collection, narrative curiosity, competition, or something else?

What is the primary player motivation?"

### 3. Boundaries

"Let's also define who this game is not for.

**Boundary questions:**

- Which player expectations should this game intentionally not satisfy?
- Which genres, difficulty levels, pacing assumptions, or content expectations are outside the design?
- What would be a misleading promise for this game?

Who is this game not for?"

### 4. First Validation

"Finally, let's define the first game validation.

**Validation questions:**

- What prototype, paper test, or playtest would prove the core experience is working?
- What player behavior would validate the intended experience?
- What player behavior would tell us the concept is failing?

What is the first validation test?"

### 5. Generate Player Fit Content

Based on the conversation, prepare the content:

```markdown
## Player and Experience Fit

### Intended Player Experience

{{intended_player_experience}}

### Primary Player Motivation

{{primary_player_motivation}}

### Secondary Appeal

{{secondary_appeal}}

### Not For

{{not_for}}

### First Game Validation

{{first_validation}}
```

### 6. Present Content and Menu

Show the generated content to the user and present:

"I've drafted the Player and Experience Fit section based on our conversation.

**Here's what I'll add to the document:**

[Show the complete markdown content from step 5]

**Validation Check:**

- Is the intended player experience specific enough to guide design decisions?
- Are the motivations tied to actual mechanics or session behavior?
- Is the first validation test practical?

**Do not present per-section options. Update `preproduction/design.md` and continue the stage.**
Edit/refinement: apply corrections directly to `preproduction/design.md`.
Stage boundary: use CONTINUE only after the complete game-conception stage is ready.

### 7. Handle Menu Selection

#### If the player refines:

- Ask targeted follow-up questions about weak, vague, risky, or incomplete parts of the current draft.
- Revise the current content in place using the user's answers.
- Apply the refinement directly to preproduction/design.md and continue the stage.

#### Do not use CONTINUE inside the stage:

- Append the final content to `{outputFile}`
- Replace the existing Player and Experience Fit section in `{outputFile}` if it already exists.
- Update frontmatter: `stepsCompleted: [1, 2, 3]`
- Load `{nextStepFile}`

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [CONTINUE option] is selected and [player fit content saved with frontmatter updated], will you then load and read fully `{nextStepFile}`.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Intended player experience is specific and design-useful
- Primary player motivation is clear
- Non-fit boundaries are explicit
- First validation test is practical
- REFINE/CONTINUE menu presented and handled correctly
- Frontmatter updated with stepsCompleted: [1, 2, 3]

### SYSTEM FAILURE:

- Asking non-game business questions
- Generating player assumptions without user input
- Player definition is too vague to guide decisions
- Waiting for per-section CONTINUE before writing or proceeding

