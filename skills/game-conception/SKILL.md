---
name: game-conception
description: Create the single game brief for a new game with a compact conception sequence, concept-depth checks, validation, and feasibility review.
---

# AGDA: Game Conception

Use this skill for the first creative preproduction stage of a new game. It creates one output file:

```text
preproduction/design.md
```

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Source Rules

Use the workflow below as the authority. Local reference material may inform phrasing or checks, but this skill must not require any external repository, agent, script, configuration folder, or brand-specific workflow to run.

## Method

Use this game brief sequence as the spine, in this order:

1. Initialization / resume
2. Game Vision
3. Player and Experience Fit
4. Game Fundamentals
5. Scope and Constraints
6. Reference Framework
7. Content and Production
8. Core Loop Design
9. MDA and Player Motivation
10. Pillars and Anti-Pillars
11. Scope Feasibility and MVP
12. Final Review and Next Action

After Content and Production, run the concept-depth pieces as guided steps. Do not silently fill them:

- Core loop design: moment-to-moment, short-term, session, long-term progression.
- Pillars and anti-pillars: each pillar needs a design test; anti-pillars define what this game is not.
- Player validation: intended player experience, primary player motivation, secondary appeal, who the game is not for, autonomy, competence, and relatedness.
- MDA and player motivation: target aesthetics, intended dynamics, core mechanics, autonomy, competence, relatedness, and flow-state notes.
- Scope and feasibility: target platform, engine preference if known, art pipeline complexity, broad content scale, technical risks, MVP, biggest risks, and scope tiers.

Keep the 12 sections exclusive:

- Step 4 owns player fantasy, primary mechanics, and experience goals only. Do not define final pillars there.
- Step 5 owns constraints and explicit exclusions only. Do not define MVP, scope tiers, or cut lines there.
- Step 10 is the only place for pillars, anti-pillars, design tests, and pillar conflict priority.
- Step 11 is the only place for MVP definition, feasibility, scope tiers, and cut lines.
- Step 12 is the only place for final non-goals, risks, and next stage.

## Collaboration

- Act as a facilitator, not a silent generator.
- Never fill a section without real user input or existing project evidence.
- For each step, draft from existing context, previous answers, and project evidence, then write or update `preproduction/design.md` immediately.
- Do not post full section drafts into chat by default. Chat should summarize what changed and ask the next focused question.
- Do not ask the player to approve every section or every bit.
- Do not use `REFINE` / `CONTINUE` menus inside the stage.
- If the player corrects or refines something, edit `preproduction/design.md` directly and continue the stage.
- Ask a focused clarification only when the draft cannot be made from available context without inventing important facts.
- Ask required decisions during the process. Do not leave a question backlog or unresolved decision list in `preproduction/design.md`.
- Challenge vague claims, especially player fantasy, experience goals, differentiators, pillars, MVP, and scope.
- Do not run research workflows unless the user explicitly asks.
- `CONTINUE` is only meaningful after this whole stage is complete, when the player wants to move to the recommended next skill.
- Broad content, world, narrative, art, audio, and production direction are part of the brief.
- Do not force exact MVP or production content lists during conception. Avoid prompts that require specific buildings, level counts, map lists, mission lists, character rosters, enemy rosters, item/weapon catalogs, quest/dialogue/story-beat lists, asset lists, UI screen lists, or gameplay-hour targets.
- If exact content detail seems necessary, convert it into a broad category or representative scope statement and continue with the game idea, brief, and systems-level framing.
- Do not create extra top-level sections or subsections outside the canonical 12-section template. If a topic starts becoming a system design, record it briefly under `Systems Mapping Candidates` in Step 11 and leave the details for `systems-mapping` and `system-design`.
- Do not write `TBD`, `unknown`, or placeholder values into `preproduction/design.md`. Ask during the process if the field is required; otherwise omit the line or write a resolved neutral statement such as `Not central to MVP`.
- Frontmatter must use canonical numeric progress only: `stepsCompleted: [1, 2, ...]` and `lastStep: 1-12`. Never put topic names, system names, or custom step slugs in frontmatter.

## Output Shape

Use `../../docs/templates/design.md` as the compact shape. The file is the game brief. Do not create separate concept, pillars, or player-profile files unless the user explicitly asks.

`preproduction/design.md` is the artifact other AGDA stages consume. For every step:

- Create or update `preproduction/design.md` immediately after the player's answer gives enough information.
- Replace the relevant section if it already exists; do not append duplicate sections.
- Update frontmatter with `stepsCompleted` and `lastStep`.
- Keep chat concise: say which file and section changed, then continue the guided journey.
- Do not proceed to `systems-mapping` until `preproduction/design.md` exists and contains the completed brief.

## Done When

`preproduction/design.md` contains:

- Core concept, pitch, vision, core fantasy, and unique hook.
- Player definition and player validation.
- Primary mechanics, experience goals, constraints, references, differentiators, high-level content direction, and production constraints.
- Core loops, MDA/motivation analysis, pillars, anti-pillars, feasibility notes, and scope tiers.
- MVP definition, non-goals, risks, resolved assumptions/decisions, and the next AGDA stage.

## Stage Exit

When this stage is complete, end the response with:

```text
Recommended next skill: systems-mapping
```

