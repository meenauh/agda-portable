# Preproduction Workflow Reference

This file documents the old command-shaped workflow as a maintainer reference. Codex currently surfaces this plugin through skills, not custom slash commands. The visible runtime surface is the lean skill set in `skills/`; use `status-check` as the start/resume entrypoint.

## Start / Resume

Purpose: choose the next preproduction stage.

Behavior:

1. Run `status-check`: concept/design docs, systems docs, architecture docs, source code, prototypes, production artifacts.
2. If the user has a new game idea, route to New Game Preproduction.
3. If the user points to an existing repo, route to Existing Project.
4. If unclear, ask one question to choose new game vs existing project.

## New Game Preproduction

Purpose: run the complete new-game preproduction flow, stored compactly.

Outputs:

```text
preproduction/design.md
preproduction/systems.md
preproduction/architecture/technical.md
preproduction/architecture/adrs/[NNNN]-[slug].md
preproduction/architecture/reviews.md
preproduction/production-handoff.md
```

Rules:

- Ask focused questions only, but complete each stage before moving on.
- Use `game-conception` for `design.md`: full game brief plus core loop, pillars/anti-pillars, player validation, and scope/feasibility.
- Use `systems-mapping` for `systems.md`: explicit/implicit systems, acyclic dependencies, priority, and topological design order.
- Use `technical-architecture` for `architecture/technical.md`: general architecture, layers, ownership, data flow, API boundaries, read-first contracts, ADR candidates, traceability gaps, and compact review evidence in `architecture/reviews.md`.
- Use `adr-creation` after reviewed architecture for required foundation/core ADRs, keeping ADRs `Proposed` until the ADR review loop writes approval evidence in `architecture/reviews.md`.
- Use `production-handoff` for the final gate and handoff file.
- Never treat author self-review as approval. Approved/Accepted statuses require the matching review evidence in the artifact.
- Do not run separate research workflows unless explicitly requested.
- Stop before milestones, epics, stories, or code.

## Stage Detection

Purpose: detect current preproduction stage and route the next action.

Skill: `status-check`

Input:

- User prompt, repo files, existing preproduction docs.

Output:

- Project type.
- Current stage.
- Existing evidence.
- Missing blockers.
- Recommended next skill.

## Game Conception

Purpose: create or update the single game brief.

Skill: `game-conception`

Input:

- Raw game idea, existing notes, or existing `preproduction/design.md`.

Output:

```text
preproduction/design.md
```

## Systems Mapping

Purpose: map systems from the approved game brief.

Skill: `systems-mapping`

Input:

```text
preproduction/design.md
```

Output:

```text
preproduction/systems.md
```

## Technical Architecture

Purpose: create and review the general technical architecture and ADR candidate list from the approved systems map and design brief.

Skill: `technical-architecture`

Input:

```text
preproduction/design.md
preproduction/systems.md
```

Output:

```text
preproduction/architecture/technical.md
preproduction/architecture/reviews.md
```

## ADR Creation

Purpose: create and review required ADRs after technical architecture is approved.

Skill: `adr-creation`

Input:

```text
preproduction/architecture/technical.md
preproduction/design.md
preproduction/systems.md
```

Output:

```text
preproduction/architecture/adrs/[NNNN]-[slug].md
preproduction/architecture/reviews.md
```

## Existing Project

Purpose: onboard an existing game project technically.

Outputs:

```text
preproduction/project-context.md
preproduction/systems.md
preproduction/architecture/technical.md
preproduction/production-handoff.md
```

Rules:

- Inspect the repo before asking questions.
- Do not create `design.md` or per-system design docs unless the user asks for creative design work.
- Preserve existing creative and technical direction.

## Status

Purpose: report what is complete, what is missing, and the next smallest action.

Output:

- Current project type: new game or existing project.
- Existing preproduction files.
- Missing handoff gate items.
- Next skill or action.

## Production Handoff

Purpose: validate preproduction and create/update `production-handoff.md`.

Skill: `production-handoff`

Pass gate:

- New game: game brief, systems map, reviewed technical architecture, and reviewed accepted ADRs are present.
- Existing project: repo context, systems, architecture, and commands where discoverable are present.

Failure behavior:

- Do not create fake completeness.
- Fail artifacts that are only self-reviewed or have approved/accepted status without review notes.
- List missing items and ask only for blockers that cannot be discovered.

