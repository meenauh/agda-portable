> AGDA file-first override: write or update `preproduction/design.md` immediately when the player's answer gives enough information. Do not wait for per-section CONTINUE, do not present REFINE/CONTINUE menus inside this stage, and do not post full drafts into chat unless requested. CONTINUE is only for the stage boundary after the complete `preproduction/design.md` is ready.

---
name: 'step-11-feasibility-mvp'
description: 'Guide feasibility, MVP definition, risks, and scope tiers without production content detail'

# Path Definitions
workflow_path: '{installed_path}'

# File References
thisStepFile: './step-11-feasibility-mvp.md'
nextStepFile: './step-12-complete.md'
workflowFile: '{workflow_path}/workflow.md'
outputFile: 'preproduction/design.md'
---

# Step 11: Scope Feasibility and MVP

**Progress: Step 11 of 12** - Next: Final Review and Next Action

## STEP GOAL:

Ground the concept in platform, engine/framework, technical constraints and risks, MVP, and scope tiers.

## MANDATORY EXECUTION RULES:

- NEVER generate content without user input.
- Keep platform and engine/framework questions.
- Keep feasibility focused on platform, engine/framework, art pipeline complexity, broad content scale, and technical risks.
- Do not ask for exact MVP content lists such as specific buildings, level counts, item lists, enemy rosters, character lists, UI screen lists, audio asset lists, story beats, maps, missions, or gameplay-hour targets. Use representative categories instead.
- MVP must test whether the core loop works.
- Do not use per-section REFINE / CONTINUE. Save edits directly to preproduction/design.md.
- Do not append system-specific subsections to the brief. If a topic becomes a system design, add a one-line entry under `Systems Mapping Candidates` and leave its rules for `systems-mapping` and `system-design`.

## Sequence of Instructions

### 1. Platform and Engine / Framework

Ask:

"What platforms are you targeting, and do you already have an engine or framework preference?"

Capture:

- Target platform(s)
- Engine/framework preference, or undecided
- Platform implications for controls, performance, input, distribution, and save/network expectations

### 2. Art Pipeline and Content Scale

Draft from the existing brief:

Infer only broad content/art scale: `low`, `moderate`, or `high`.

If it cannot be inferred, ask the player for broad content/art scale during this step, not an exact content list.

Capture:

- Art pipeline complexity
- Broad content scale
- Audio direction complexity
- Procedural systems, if any

### 3. Technical and Design Risks

Ask:

"What could make this game hard to build or hard to make fun?"

Capture:

- Technical risks
- Design risks
- Content scale risks
- First validation for each

### 4. MVP Definition

Ask:

"What is the absolute minimum playable version that tests whether the core loop is fun?"

Capture:

- Core hypothesis
- Required MVP features
- Explicitly excluded features
- First playtest question

### 5. Scope Tiers

Ask:

"If we need to cut scope, what remains in MVP, what belongs in a vertical slice, and what waits until later?"

Capture:

- MVP
- Vertical slice
- Later/full vision
- Cut line

### 6. Systems Mapping Candidates

While drafting MVP and feasibility, identify concepts that should become systems later. Keep them as names plus one-line purpose only. Do not design their rules here.

### 7. Generate Feasibility Section

Prepare:

```markdown
## Scope Feasibility and MVP

### MVP Definition

Must prove:

- {{core_hypothesis}}

Required:

- {{mvp_required}}

Explicitly not in MVP:

- {{mvp_excluded}}

### Feasibility

| Area | Assessment | Risk | Cut / Mitigation |
|---|---|---|---|
| Platform | {{platform_assessment}} | {{platform_risk}} | {{platform_mitigation}} |
| Engine / framework | {{engine_assessment}} | {{engine_risk}} | {{engine_mitigation}} |
| Art pipeline | {{art_assessment}} | {{art_risk}} | {{art_mitigation}} |
| Broad content scale | {{content_scale_assessment}} | {{content_scale_risk}} | {{content_scale_mitigation}} |
| Technical risks | {{technical_assessment}} | {{technical_risk}} | {{technical_mitigation}} |

### Scope Tiers

| Tier | Game Scope | Features | Cut Line |
|---|---|---|---|
| MVP | {{mvp_scope}} | {{mvp_features}} | {{mvp_cut_line}} |
| Vertical slice | {{slice_scope}} | {{slice_features}} | {{slice_cut_line}} |
| Later | {{later_scope}} | {{later_features}} | {{later_cut_line}} |

### Systems Mapping Candidates

- {{candidate_system}}: {{one_line_purpose}}
```

### 8. Present Menu

Edit/refinement: apply corrections directly to `preproduction/design.md`.
Stage boundary: use CONTINUE only after the complete game-conception stage is ready.

### 9. Handle Selection

If the player refines, ask only the targeted follow-up needed and edit `preproduction/design.md`.

Do not use CONTINUE inside the stage; proceed by updating `preproduction/design.md` and asking the next focused question.

- Append the final section to `{outputFile}`
- Replace the existing Scope Feasibility and MVP section in `{outputFile}` if it already exists.
- Update frontmatter: `stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]`
- Load `{nextStepFile}`

