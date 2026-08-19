> AGDA file-first override: write or update `preproduction/design.md` immediately when the player's answer gives enough information. Do not wait for per-section CONTINUE, do not present REFINE/CONTINUE menus inside this stage, and do not post full drafts into chat unless requested. CONTINUE is only for the stage boundary after the complete `preproduction/design.md` is ready.

---
name: 'step-05-scope'
description: 'Define project scope including platforms, constraints, and technical boundaries'

# Path Definitions
workflow_path: '{installed_path}'

# File References
thisStepFile: './step-05-scope.md'
nextStepFile: './step-06-references.md'
workflowFile: '{workflow_path}/workflow.md'
outputFile: 'preproduction/design.md'

# Task References
---

# Step 5: Scope & Constraints

**Progress: Step 5 of 12** - Next: Reference Framework

## STEP GOAL:

Define realistic project constraints including target platforms, production boundaries, technical constraints, and explicit exclusions. Do not define MVP, scope tiers, or cut lines in this step.

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
- Push for realism about constraints
- Identify potential blockers early

### Step-Specific Rules:

- Focus on establishing realistic boundaries
- FORBIDDEN to generate scope without real user input
- Document constraints that will affect design decisions
- Do not create an MVP table, scope tiers, or cut lines here; Step 11 owns those.

## EXECUTION PROTOCOLS:

- Show your analysis before taking any action
- Do not present per-section REFINE/CONTINUE menus; update preproduction/design.md and continue the guided stage.
- Save/update preproduction/design.md immediately after the answer provides enough information.
- Update frontmatter `stepsCompleted: [1, 2, 3, 4, 5]` before loading next step

## File Update
- **REFINE**: Challenge assumptions about scope
- **CONTINUE**: Save the content and proceed

## Sequence of Instructions (Do not deviate, skip, or optimize)

### 1. Platform

**Guide user through platform selection:**

"Let's define where {{game_name}} will be played.

**Platform Considerations:**

| Platform       | Key Considerations                                      |
| -------------- | ------------------------------------------------------- |
| **PC**         | Keyboard/mouse, broad hardware range, flexible input    |
| **Console**    | Controller-first, certification, couch play             |
| **Mobile**     | Touch controls, short sessions, performance and store constraints |
| **Web**        | Instant access, file size limits, browser compatibility |
| **VR**         | Specialized hardware, motion controls, comfort          |

**Questions to consider:**

- Where does the intended play experience work best?
- Which platform(s) are you targeting for launch?
- Are there secondary platforms for later?

What platform(s) are you targeting for {{game_name}}?"

### 2. Technical Constraints

**Identify technical boundaries:**

"Finally, let's identify technical constraints.

**Technical Considerations:**

- **Engine/framework:** Already decided or open?
- **Performance targets:** Frame rate, file size, load times?
- **Accessibility:** What accessibility features are required?
- **Online features:** Multiplayer, leaderboards, cloud saves?

What technical constraints apply to {{game_name}}?"

### 5. Generate Scope Content

Based on the conversation, prepare the content:

```markdown
## Scope and Constraints

### Target Platforms

**Primary:** {{primary_platform}}
**Secondary:** {{secondary_platforms}}

### Technical Constraints

{{technical_constraints}}

### Scope Realities

{{scope_acknowledgements}}

### Explicit Exclusions

{{explicit_exclusions}}
```

### 6. Present Content and Menu

Show the generated content to the user and present:

"I've drafted the Scope & Constraints section based on our conversation.

**Here's what I'll add to the document:**

[Show the complete markdown content from step 5]

**Validation Check:**

- Are these constraints realistic?
- Have we identified potential blockers?
- Is the scope achievable with these production boundaries?

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
- Replace the existing Scope and Constraints section in `{outputFile}` if it already exists.
- Update frontmatter: `stepsCompleted: [1, 2, 3, 4, 5]`
- Load `{nextStepFile}`

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [CONTINUE option] is selected and [scope content saved with frontmatter updated], will you then load and read fully `{nextStepFile}`.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Target platforms clearly defined
- Technical constraints established
- REFINE/CONTINUE menu presented and handled correctly
- Frontmatter updated with stepsCompleted: [1, 2, 3, 4, 5]

### SYSTEM FAILURE:

- Generating scope without user input
- Unrealistic constraints that set project up for failure
- Missing critical blockers
- Waiting for per-section approval instead of updating preproduction/design.md
- Waiting for per-section CONTINUE before writing or proceeding

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.




