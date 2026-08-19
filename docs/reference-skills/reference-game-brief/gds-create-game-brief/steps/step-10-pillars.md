> AGDA file-first override: write or update `preproduction/design.md` immediately when the player's answer gives enough information. Do not wait for per-section CONTINUE, do not present REFINE/CONTINUE menus inside this stage, and do not post full drafts into chat unless requested. CONTINUE is only for the stage boundary after the complete `preproduction/design.md` is ready.

---
name: 'step-10-pillars'
description: 'Guide game pillars, anti-pillars, and conflict priority'

# Path Definitions
workflow_path: '{installed_path}'

# File References
thisStepFile: './step-10-pillars.md'
nextStepFile: './step-11-feasibility-mvp.md'
workflowFile: '{workflow_path}/workflow.md'
outputFile: 'preproduction/design.md'
---

# Step 10: Pillars and Anti-Pillars

**Progress: Step 10 of 12** - Next: Scope Feasibility and MVP

## STEP GOAL:

Define 3-5 concrete game pillars, their design tests, anti-pillars, and conflict priority.

## MANDATORY EXECUTION RULES:

- NEVER generate pillars without user input.
- Pillars must be falsifiable and constraining. Reject generic pillars like "fun gameplay" or "good art".
- Each pillar needs a design test that would resolve a real decision.
- Anti-pillars must exclude plausible temptations, not obvious irrelevant things.
- Do not use per-section REFINE / CONTINUE. Save edits directly to preproduction/design.md.

## Sequence of Instructions

### 1. Pillar Candidates

Ask:

"Based on the brief, content direction, core loop, and MDA analysis, what are the 3-5 non-negotiable principles this game must protect?"

For each pillar, capture:

- Name
- One-sentence meaning
- Target feeling or motivation it serves
- Design test
- Production implication

### 2. Anti-Pillars

Ask:

"What tempting directions should this game explicitly not pursue because they would weaken the core experience?"

Capture at least three anti-pillars in this form:

- NOT [thing], because it would compromise [pillar or core loop]

### 3. Conflict Priority

Ask:

"When pillars conflict, which one wins first, second, and third? Give the reason for the priority."

### 4. Generate Pillars Section

Prepare:

```markdown
## Pillars and Anti-Pillars

| Pillar | Meaning | Design Test | Production Implication |
|---|---|---|---|
| {{pillar_1}} | {{meaning_1}} | {{test_1}} | {{implication_1}} |
| {{pillar_2}} | {{meaning_2}} | {{test_2}} | {{implication_2}} |
| {{pillar_3}} | {{meaning_3}} | {{test_3}} | {{implication_3}} |

### Anti-Pillars

- {{anti_pillar_1}}
- {{anti_pillar_2}}
- {{anti_pillar_3}}

### Pillar Conflict Priority

1. {{priority_1}}
2. {{priority_2}}
3. {{priority_3}}
```

### 5. Present Menu

Edit/refinement: apply corrections directly to `preproduction/design.md`.
Stage boundary: use CONTINUE only after the complete game-conception stage is ready.

### 6. Handle Selection

If the player refines, ask only the targeted follow-up needed and edit `preproduction/design.md`.

Do not use CONTINUE inside the stage; proceed by updating `preproduction/design.md` and asking the next focused question.

- Append the final section to `{outputFile}`
- Replace the existing Pillars and Anti-Pillars section in `{outputFile}` if it already exists.
- Update frontmatter: `stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]`
- Load `{nextStepFile}`

