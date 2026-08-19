> AGDA file-first override: write or update `preproduction/design.md` immediately when the player's answer gives enough information. Do not wait for per-section CONTINUE, do not present REFINE/CONTINUE menus inside this stage, and do not post full drafts into chat unless requested. CONTINUE is only for the stage boundary after the complete `preproduction/design.md` is ready.

---
name: 'step-09-mda-motivation'
description: 'Guide MDA analysis and player motivation checks'

# Path Definitions
workflow_path: '{installed_path}'

# File References
thisStepFile: './step-09-mda-motivation.md'
nextStepFile: './step-10-pillars.md'
workflowFile: '{workflow_path}/workflow.md'
outputFile: 'preproduction/design.md'
---

# Step 9: MDA and Player Motivation

**Progress: Step 9 of 12** - Next: Pillars and Anti-Pillars

## STEP GOAL:

Translate the intended player experience into target aesthetics, dynamics, mechanics, and motivation checks.

## MANDATORY EXECUTION RULES:

- NEVER generate content without user input.
- Keep the framework practical; use it to sharpen design decisions, not to create academic filler.
- Ask for the top 2-3 aesthetics only, then map them to dynamics and mechanics.
- Do not use per-section REFINE / CONTINUE. Save edits directly to preproduction/design.md.

## Sequence of Instructions

### 1. Target Aesthetics

Ask:

"Which 2-3 feelings should dominate the player experience?"

Use these categories as prompts, not a required checklist:

- Sensation: sensory pleasure
- Fantasy: inhabiting a role or world
- Narrative: drama or story arc
- Challenge: mastery and obstacles
- Fellowship: connection with others
- Discovery: exploration and secrets
- Expression: creativity or identity
- Submission: relaxing flow or comfort

### 2. Intended Dynamics

Ask:

"What should players naturally start doing because of the rules? For example: experimenting, optimizing, exploring, planning, improvising, cooperating, competing, or roleplaying."

### 3. Core Mechanics

Ask:

"Which mechanics create those dynamics and feelings? Name only the systems that directly support the intended experience."

### 4. Motivation Check

Ask:

"How does the game serve autonomy, competence, and relatedness?"

Capture:

- Autonomy: meaningful choice and agency
- Competence: mastery, skill growth, clear feedback
- Relatedness: connection to characters, world, community, or other players

### 5. Flow Check

Ask:

"How does the game keep challenge matched to player skill? Consider onboarding, feedback clarity, difficulty growth, and recovery from failure."

### 6. Generate MDA and Motivation Section

Prepare:

```markdown
## MDA and Player Motivation

### MDA

| Layer | Notes |
|---|---|
| Target aesthetics | {{target_aesthetics}} |
| Intended dynamics | {{intended_dynamics}} |
| Core mechanics | {{core_mechanics}} |

### Motivation

| Need | How The Game Serves It | Strength |
|---|---|---|
| Autonomy | {{autonomy}} | {{autonomy_strength}} |
| Competence | {{competence}} | {{competence_strength}} |
| Relatedness | {{relatedness}} | {{relatedness_strength}} |

- **Flow-state notes:** {{flow_notes}}
- **Player motivation fit:** {{motivation_fit}}
```

### 7. Present Menu

Edit/refinement: apply corrections directly to `preproduction/design.md`.
Stage boundary: use CONTINUE only after the complete game-conception stage is ready.

### 8. Handle Selection

If the player refines, ask only the targeted follow-up needed and edit `preproduction/design.md`.

Do not use CONTINUE inside the stage; proceed by updating `preproduction/design.md` and asking the next focused question.

- Append the final section to `{outputFile}`
- Replace the existing MDA and Player Motivation section in `{outputFile}` if it already exists.
- Update frontmatter: `stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8, 9]`
- Load `{nextStepFile}`

