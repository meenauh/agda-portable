> AGDA file-first override: write or update `preproduction/design.md` immediately when the player's answer gives enough information. Do not wait for per-section CONTINUE, do not present REFINE/CONTINUE menus inside this stage, and do not post full drafts into chat unless requested. CONTINUE is only for the stage boundary after the complete `preproduction/design.md` is ready.

---
name: 'step-04-fundamentals'
description: 'Define player fantasy, primary mechanics, and player experience goals'

# Path Definitions
workflow_path: '{installed_path}'

# File References
thisStepFile: './step-04-fundamentals.md'
nextStepFile: './step-05-scope.md'
workflowFile: '{workflow_path}/workflow.md'
outputFile: 'preproduction/design.md'

# Task References
---

# Step 4: Game Fundamentals

**Progress: Step 4 of 12** - Next: Scope & Constraints

## STEP GOAL:

Define player fantasy, primary mechanics (what players do), and player experience goals (what feelings are designed for). Do not define final pillars in this step.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER generate content without user input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with CONTINUE, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- NEVER mention time estimates
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are a veteran game designer facilitator collaborating with a creative peer
- Connect mechanics directly to emotional experiences

### Step-Specific Rules:

- Focus on the core of what makes this game unique
- FORBIDDEN to generate fundamentals without real user input
- Do not create pillars, anti-pillars, design tests, or pillar priority here; those belong only in Step 10.
- Focus on player actions rather than implementation details

## EXECUTION PROTOCOLS:

- Show your analysis before taking any action
- Do not present per-section REFINE/CONTINUE menus; update preproduction/design.md and continue the guided stage.
- Save/update preproduction/design.md immediately after the answer provides enough information.
- Update frontmatter `stepsCompleted: [1, 2, 3, 4]` before loading next step

## File Update
- **REFINE**: Stress test the fundamentals
- **CONTINUE**: Save the content and proceed

## Sequence of Instructions (Do not deviate, skip, or optimize)

### 1. Player Fantasy

Ask:

"What should the player feel they are becoming, mastering, or expressing in {{game_name}}?"

Capture:

- Player role or fantasy.
- What the player is trying to get better at.
- What should feel satisfying before long-term progression exists.

### 2. Primary Mechanics

**Explore what players actually do:**

"Now let's define what players actually DO in {{game_name}}.

**Think in verbs - what actions define the experience?**

Examples:

- Jump, dash, climb (movement)
- Attack, dodge, parry (combat)
- Craft, build, place (creation)
- Talk, choose, influence (social)
- Collect, trade, manage (economy)

**Questions to consider:**

- What's the core action players repeat most often?
- What actions create the most satisfying moments?
- How do different mechanics interact?

What are the primary mechanics in {{game_name}}?"

### 3. Experience Goals

**Define the emotional targets:**

"Finally, let's define the player experience goals - what feelings are you designing for?

**Emotional Experience Framework:**

| Emotion                   | Examples                               |
| ------------------------- | -------------------------------------- |
| **Tension/Relief**        | Horror games, difficult boss fights    |
| **Mastery/Growth**        | Skill-based games, RPG progression     |
| **Creativity/Expression** | Sandbox games, character customization |
| **Exploration/Surprise**  | Exploration games, mystery narratives  |
| **Connection/Belonging**  | Multiplayer, community-driven games    |
| **Relaxation/Flow**       | Cozy games, rhythm games               |

**Questions to consider:**

- What feeling do you want players to have after a session?
- What emotional journey happens during play?
- What makes this experience meaningful?

What are the player experience goals for {{game_name}}?"

### 4. Generate Fundamentals Content

Based on the conversation, prepare the content:

```markdown
## Game Fundamentals

### Player Fantasy

{{player_fantasy}}

### Primary Mechanics

{{mechanics_list_with_descriptions}}

**Core Loop:** {{how_mechanics_combine_into_loop}}

### Player Experience Goals

{{experience_goals}}

**Emotional Journey:** {{what_players_feel_during_play}}
```

### 5. Present Content and Menu

Show the generated content to the user and present:

"I've drafted the Game Fundamentals section based on our conversation.

**Here's what I'll add to the document:**

[Show the complete markdown content from step 4]

**Validation Check:**

- Is the player fantasy specific enough to guide design?
- Do mechanics support the intended player experience?
- Do experience goals match the intended player experience?

**Do not present per-section options. Update `preproduction/design.md` and continue the stage.**
Edit/refinement: apply corrections directly to `preproduction/design.md`.
Stage boundary: use CONTINUE only after the complete game-conception stage is ready.

### 6. Handle Menu Selection

#### If the player refines:

- Ask targeted follow-up questions about weak, vague, risky, or incomplete parts of the current draft.
- Revise the current content in place using the user's answers.
- Apply the refinement directly to preproduction/design.md and continue the stage.

#### Do not use CONTINUE inside the stage:

- Append the final content to `{outputFile}`
- Replace the existing Game Fundamentals section in `{outputFile}` if it already exists.
- Update frontmatter: `stepsCompleted: [1, 2, 3, 4]`
- Load `{nextStepFile}`

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [CONTINUE option] is selected and [fundamentals content saved with frontmatter updated], will you then load and read fully `{nextStepFile}`.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Player fantasy is clear
- Primary mechanics clearly described
- Experience goals tied to player fit and vision
- REFINE/CONTINUE menu presented and handled correctly
- Frontmatter updated with stepsCompleted: [1, 2, 3, 4]

### SYSTEM FAILURE:

- Generating fundamentals without user input
- Generic mechanics or experience goals that don't guide decisions
- Mechanics disconnected from experience goals
- Waiting for per-section approval instead of updating preproduction/design.md
- Waiting for per-section CONTINUE before writing or proceeding

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.




