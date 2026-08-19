---
name: system-design
description: Design the next unfinished epic from the approved system map and architecture baseline before story shaping.
---

# AGDA: System Design

Use this skill during production after `production-planning` has created an epic and the epic is ready for design refinement.

It creates or updates:

```text
production/designs/[SYSTEM].md
production/epics/EPIC-###.md
production/backlog.md
production/status.md
```

## Git Worktree Boundary

Run only in the active request worktree recorded by `requests-intake` in `production/status.md`. Write no production artifact from the primary `develop` checkout. Keep the request branch unmerged until final work approval.

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Source Rules

Use the local reference material as the authority for this stage:

- `plugins/AGDA/docs/reference-templates/templates/technical-design-document.md`
- `plugins/AGDA/docs/reference-templates/templates/game-design-document.md`
- `plugins/AGDA/docs/reference-templates/templates/architecture-traceability.md`

Use the current production artifacts first:

- `production/plan.md`
- `production/backlog.md`
- `production/status.md`
- existing `production/designs/*.md` files for the same system or feature
- the matching epic row in `production/backlog.md`
- the epic document at `production/epics/EPIC-###.md`
- `preproduction/systems.md`
- `preproduction/architecture/technical.md`
- `preproduction/architecture/reviews.md`
- any approved ADRs that shape the epic

## Method

Design the selected epic in one bounded pass. Focus on the epic's intended outcome, scope, constraints, dependencies, validation shape, and implementation risks. Do not break the epic into stories or tasks here.

Read the existing design doc, if one exists, then the epic row, the epic document, and the architecture baseline before writing. If the system already has a design doc, update that doc with the new information and append a dated log entry at the end. If the system is new, create a new design doc under `production/designs/` using the technical design template. If the epic depends on a new or changed design decision that is not already covered by the baseline architecture or an approved ADR, record that in the epic as an architecture follow-up requirement and route to `technical-architecture` after the design pass.

Keep the epic design compact and decision-oriented:

- epic intent and player/operator outcome
- scope boundaries and non-goals
- dependencies and sequencing constraints
- validation or playtest shape
- architecture touchpoints
- any story-shaping guidance that narrows later decomposition

Update the design doc as the source of truth for production design. Keep the epic document as a reference index only during design: point it at the relevant design doc, ADRs, and any follow-up notes. Keep story and task sections empty until `story-shaping` runs.

Update `production/status.md` with the current epic, the design status, and the next required skill.

## Boundaries

- Do not create story/task breakdown here.
- Do not create separate design documents.
- Do not edit preproduction design docs for production design work.
- Do not put production design prose in the epic; use the production design doc instead.
- Do not write preproduction system docs.
- Do not reopen the whole game baseline unless the epic genuinely changes the approved system map or architecture baseline.

## Done When

The selected epic has compact design notes in `production/epics/EPIC-###.md`, the backlog/status point at the next step, and any architecture follow-up requirement is explicit.

## Stage Exit

If the epic is ready for review:

```text
Recommended next skill: system-design-review
```

If the epic needs an architecture check or ADR before shaping:

```text
Recommended next skill: technical-architecture
```

If the epic is already designed and ready for story shaping:

```text
Recommended next skill: story-shaping
```

