> AGDA file-first override: write or update `preproduction/design.md` immediately when the player's answer gives enough information. Do not wait for per-section CONTINUE, do not present REFINE/CONTINUE menus inside this stage, and do not post full drafts into chat unless requested. CONTINUE is only for the stage boundary after the complete `preproduction/design.md` is ready.

---
name: 'step-12-complete'
description: 'Finalize the game brief and route to the next AGDA stage'

# Path Definitions
workflow_path: '{installed_path}'

# File References
thisStepFile: './step-12-complete.md'
workflowFile: '{workflow_path}/workflow.md'
outputFile: 'preproduction/design.md'

# Workflow References
nextWorkflow: 'skill:systems-mapping'
---

# Step 12: Final Review and Next Action

**Progress: Step 12 of 12** - Game Brief Complete!

## STEP GOAL:

Finalize non-goals, risks, required decisions, and the next AGDA stage.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER generate content without user input
- CRITICAL: Read the complete step file before taking any action
- YOU ARE A FACILITATOR, not a content generator
- NEVER mention time estimates
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are a veteran game designer facilitator collaborating with a creative peer
- This is the final step - ensure completeness
- Provide one actionable next stage

### Step-Specific Rules:

- Do not add outcome metrics.
- Do not ask the player a questionnaire before showing the final draft.
- Draft the final review from existing brief content first, then ask for REFINE or CONTINUE.
- Keep the next action to systems mapping.
- Do not create new design subsections in final review. If a new system-level insight appears, add it to Step 11 `Systems Mapping Candidates` before finalizing.
- Remove any `TBD`, placeholder, empty section, or non-canonical extra heading before declaring the brief complete.

## EXECUTION PROTOCOLS:

- Generate the final review draft from the completed brief
- Save or update preproduction/design.md before summarizing changes in chat
- Update frontmatter `stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]`
- Present completion summary and next stage

## Sequence of Instructions (Do not deviate, skip, or optimize)

### 1. Draft Non-Goals, Risks, and Required Decisions

Using the completed brief, draft:

- Non-goals: things production must not accidentally expand.
- Risks: design, technical, content, pipeline, or scope risks already implied by the brief.
- Blockers: only blockers that prevent systems mapping.

If an important item cannot be inferred and blocks systems mapping, ask the player during this step and update `preproduction/design.md` with the resolved decision. Do not leave unresolved decision backlogs in the document.

### 2. Generate Executive Summary

**Create summary section:**

Based on all previous sections, synthesize an executive summary:

```markdown
## Executive Summary

{{game_name}} is {{core_concept}}.

**Player Experience:** {{intended_player_experience_summary}}

**Core Pillars:** {{pillars_list}}

**Key Differentiators:** {{top_differentiators}}

**Platform:** {{primary_platform}}
```

### 3. Generate Final Review and Next Action Content

Based on the completed brief, prepare the content:

```markdown
## Final Review and Next Action

### Non-Goals

{{non_goals}}

### Risks

{{risk_table}}

### Next AGDA Stage

Systems mapping from this approved brief.
```

### 4. Present Draft and Menu

Show the final review draft to the player.

Edit/refinement: apply corrections directly to `preproduction/design.md`.
Stage boundary: use CONTINUE only after the complete game-conception stage is ready.

### 5. Handle Draft Selection

**If the player refines:**

- Apply the player's edits.
- Present the revised final review again.
- Return to REFINE / CONTINUE.

**Do not use CONTINUE inside the stage:**

- Save the final review.
- Replace the existing Final Review and Next Action section in `{outputFile}` if it already exists.
- Update frontmatter with final `stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]`
- Continue to the completion summary.

### 6. Present Completion Summary

"**Game Brief Complete!**

{{user_name}}, the Game Brief for **{{game_name}}** is now complete!

**Brief Summary:**

- **Core Concept:** {{core_concept}}
- **Player Experience:** {{intended_player_experience}}
- **Pillars:** {{pillars}}
- **Platform:** {{platform}}

**Sections Completed:**

1. Initialization
2. Game Vision
3. Player and Experience Fit
4. Game Fundamentals
5. Scope & Constraints
6. Reference Framework
7. Content and Production
8. Core Loop Design
9. MDA and Player Motivation
10. Pillars and Anti-Pillars
11. Scope Feasibility and MVP
12. Final Review and Next Action

**Document saved to:** `{outputFile}`

Do you want to review or adjust anything before we finalize?"

### 7. Present Next Stage

**After user confirms completion:**

"**Recommended Next AGDA Stage for {{game_name}}:**

Run `systems-mapping`.

- **Input:** `preproduction/design.md`
- **Output:** `preproduction/systems.md`
- **Purpose:** decompose the approved brief into explicit systems, dependencies, priority tiers, and design order.

Edit/refinement: apply corrections directly to `preproduction/design.md`.
Stage boundary: use CONTINUE only after the complete game-conception stage is ready.

### 8. Handle User Selection

Based on user choice:

**Do not use CONTINUE inside the stage:**

- Update frontmatter with final `stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]`
- Route to `systems-mapping`

**If the player refines:**

- Present full document summary
- Ask what section to adjust, then update the brief before returning to this completion step

## CRITICAL STEP COMPLETION NOTE

This is the final step. Ensure:

- Executive summary is generated
- All sections are saved to `preproduction/design.md`
- Frontmatter shows all 12 steps completed
- Frontmatter uses only canonical numeric progress: `stepsCompleted: [1, 2, ..., 12]` and `lastStep: 12`
- User has clear actionable next steps
- Next AGDA stage is systems mapping

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Non-goals are explicit
- Required decisions are resolved during the process
- Executive summary synthesizes the brief
- Document is complete and saved
- Clear next stage provided
- Frontmatter updated with all steps completed

### SYSTEM FAILURE:

- Adding outcome metrics
- No clear next stage
- Frontmatter not updated to show completion
- User left without actionable guidance

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.

---

## Game Brief Workflow Complete

The Game Brief workflow transforms a game idea into a validated vision through 12 collaborative steps:

1. **Initialize** - Set up workflow and discover input documents
2. **Vision** - Capture core concept, pitch, and vision statement
3. **Player Fit** - Define intended player experience and validation assumptions
4. **Fundamentals** - Establish player fantasy, mechanics, and experience goals
5. **Scope** - Set platform and technical constraints
6. **References** - Identify inspirations and differentiators
7. **Content** - Define world, art/audio, broad content scale, and production approach
8. **Core Loop** - Define moment, short-term, session, and progression loops
9. **MDA and Motivation** - Map aesthetics, dynamics, mechanics, and player needs
10. **Pillars** - Define pillars, design tests, anti-pillars, and conflict priority
11. **Feasibility and MVP** - Ground platform, engine/framework, broad content scale, risks, MVP, and scope tiers
12. **Complete** - Final review and route to systems mapping

This step-file architecture ensures consistent, thorough game brief creation with user collaboration at every step.

## On Complete

Do not create the production handoff here. The production handoff is a separate final preproduction stage after systems mapping, system GDDs, design reviews, technical architecture, and required ADRs are complete.


