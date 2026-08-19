> AGDA file-first override: write or update `preproduction/design.md` immediately when the player's answer gives enough information. Do not wait for per-section CONTINUE, do not present REFINE/CONTINUE menus inside this stage, and do not post full drafts into chat unless requested. CONTINUE is only for the stage boundary after the complete `preproduction/design.md` is ready.

---
name: 'step-02-vision'
description: 'Define the core game vision including name, concept, pitch, and vision statement'

# Path Definitions
workflow_path: '{installed_path}'

# File References
thisStepFile: './step-02-vision.md'
nextStepFile: './step-03-market.md'
workflowFile: '{workflow_path}/workflow.md'
outputFile: 'preproduction/design.md'

# Task References
---

# Step 2: Game Vision

**Progress: Step 2 of 12** - Next: Player and Experience Fit

## STEP GOAL:

Capture the core game vision including the working title, one-sentence concept, elevator pitch, and aspirational vision statement that will guide all design decisions.

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
- Vision is the foundation - get it right before moving forward
- Challenge vague language and elevate compelling ideas

### Step-Specific Rules:

- Focus on crystallizing the game's core identity
- FORBIDDEN to generate vision without real user input
- Push for specificity and clarity
- Reference successful games as examples of good pitches

## EXECUTION PROTOCOLS:

- Show your analysis before taking any action
- Do not present per-section REFINE/CONTINUE menus; update preproduction/design.md and continue the guided stage.
- Save/update preproduction/design.md immediately after the answer provides enough information.
- Update frontmatter `stepsCompleted: [1, 2]` before loading next step
- FORBIDDEN to load next step until CONTINUE is selected

## File Update
- **REFINE**: Dig deeper into the vision
- **CONTINUE**: Save the content to the document and proceed to next step

## Sequence of Instructions (Do not deviate, skip, or optimize)

### 1. Game Name

**Start with the basics:**

"Let's start with your game's identity.

**What's the working title for your game?**

(Don't worry if it's not final - working titles help us talk about the game and can always change later.)"

Store in frontmatter: `game_name: '{user_provided_name}'`

### 2. Context Check

**If input documents were loaded:**

"I've reviewed your {brainstorming/research} documents and noticed some interesting ideas:

{summarize_key_themes_from_documents}

Let's use these as a starting point for crystallizing your vision."

### 3. Core Concept

**Guide user through concept definition:**

"Now let's capture the essence of {{game_name}} in a single sentence.

**Examples of great one-sentence concepts:**

- 'A roguelike deck-builder where you climb a mysterious spire' (Slay the Spire)
- 'A precision platformer about climbing a mountain and overcoming anxiety' (Celeste)
- 'A cozy farming sim where you rebuild your grandfather's farm and become part of a small town' (Stardew Valley)

**What is {{game_name}}?** Give me one sentence that captures the core experience."

### 4. Elevator Pitch

**Build on the concept:**

"Now let's expand that into an elevator pitch - 2-3 sentences that would compel a player or publisher to want to know more.

**A great elevator pitch answers:**

- What is it? (genre, style)
- What do you do? (core action)
- What makes it special? (hook)

**Refine this until it hooks attention.** What's your elevator pitch for {{game_name}}?"

### 5. Vision Statement

**Explore the aspirational vision:**

"Finally, let's capture your aspirational vision - the experience you want to create and what makes it meaningful.

**Questions to consider:**

- What feeling do you want players to have when they put down the controller?
- What would make this game matter to someone?
- What's your personal motivation for making this?

**This is your North Star** - ambitious yet achievable. What's your vision for {{game_name}}?"

### 6. Generate Vision Content

Based on the conversation, prepare the content:

```markdown
## Game Vision

### Core Concept

{{core_concept}}

### Elevator Pitch

{{elevator_pitch}}

### Vision Statement

{{vision_statement}}
```

### 7. Present Content and Menu

Show the generated content to the user and present:

"I've drafted the Game Vision section based on our conversation.

**Here's what I'll add to the document:**

[Show the complete markdown content from step 6]

**Validation Check:**

- Does the core concept capture the essence?
- Does the pitch hook attention?
- Does the vision inspire?

**Do not present per-section options. Update `preproduction/design.md` and continue the stage.**
Edit/refinement: apply corrections directly to `preproduction/design.md`.
Stage boundary: use CONTINUE only after the complete game-conception stage is ready.

### 8. Handle Menu Selection

#### If the player refines:

- Ask targeted follow-up questions about weak, vague, risky, or incomplete parts of the current draft.
- Revise the current content in place using the user's answers.
- Apply the refinement directly to preproduction/design.md and continue the stage.

#### Do not use CONTINUE inside the stage:

- Append the final content to `{outputFile}`
- Replace the existing Game Vision section in `{outputFile}` if it already exists.
- Update frontmatter: `stepsCompleted: [1, 2]`, `game_name: '{game_name}'`
- Load `{nextStepFile}`

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [CONTINUE option] is selected and [vision content saved with frontmatter updated including game_name], will you then load and read fully `{nextStepFile}`.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Game name captured and stored in frontmatter
- Core concept is clear and concise (one sentence)
- Elevator pitch is compelling (2-3 sentences)
- Vision statement is aspirational yet achievable
- REFINE/CONTINUE menu presented and handled correctly
- Frontmatter updated with stepsCompleted: [1, 2]

### SYSTEM FAILURE:

- Generating vision without user input
- Core concept is vague or generic
- Elevator pitch doesn't hook attention
- Waiting for per-section approval instead of updating preproduction/design.md
- Waiting for per-section CONTINUE before writing or proceeding

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.




