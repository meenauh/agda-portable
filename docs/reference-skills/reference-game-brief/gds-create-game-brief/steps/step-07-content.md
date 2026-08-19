---
name: gds-create-game-brief-step-07-content-production
description: 'Capture high-level content, art/audio direction, and production approach without exact content lists'
step: 7
workflow: gds-create-game-brief
nextStepFile: './step-08-core-loop.md'
outputFile: 'preproduction/design.md'
---

# Step 7: Content and Production

> AGDA file-first override: write or update `preproduction/design.md` immediately when the player's answer gives enough information. Do not wait for per-section CONTINUE, do not present REFINE/CONTINUE menus inside this stage, and do not post full drafts into chat unless requested. CONTINUE is only for the stage boundary after the complete `preproduction/design.md` is ready.

## Purpose

Capture broad content direction and production implications that shape the game idea, scope, and later systems mapping.

This is not detailed content planning. Do not require exact lists of levels, buildings, biomes, maps, missions, characters, enemies, bosses, items, weapons, quests, dialogue, story beats, UI screens, audio assets, visual assets, or content counts.

## Method

Infer from prior answers first. Ask only focused questions when the broad direction is missing:

- World and setting at a high level.
- Narrative approach, if relevant to the game type.
- Broad content scale: small / moderate / large. If unclear, ask for the broad scale instead of writing `unknown`.
- Visual style and production complexity.
- Audio style and production complexity.
- Production approach: prototype-first, systems-first, or content-light MVP. If unclear, ask for the broad approach instead of writing `unknown`.

If an exact MVP content detail seems necessary, convert it into a category or scope statement. For example, use "one representative building type" instead of asking "which building is there."

Write or replace this section in `preproduction/design.md`:

```markdown
## 7. Content and Production

- World and setting:
- Narrative approach:
- Broad content scale:
- Visual style:
- Audio style:
- Production approach:
```

Update frontmatter with `stepsCompleted` and `lastStep`, then continue to core loop design. Keep chat concise: say the file section was updated and ask the next focused game-design question.

