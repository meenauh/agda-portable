---
name: system-design-review
description: Review the next epic's design notes and loop with system-design until the epic is ready for architecture or shaping.
---

# AGDA: System Design Review

## Git Worktree Boundary

Run only in the active request worktree recorded by `requests-intake` in `production/status.md`. Write no production artifact from the primary `develop` checkout. Keep the request branch unmerged until final work approval.

Use this skill immediately after `system-design` completes the selected epic's design notes.

It reviews:

```text
production/designs/[SYSTEM].md
production/epics/EPIC-###.md
production/backlog.md
production/status.md
preproduction/systems.md
preproduction/architecture/technical.md
preproduction/architecture/reviews.md
approved ADRs when relevant
```

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Source Rules

Use the local reference material as the authority for this stage:

- `plugins/AGDA/docs/reference-templates/templates/technical-design-document.md`
- `plugins/AGDA/docs/reference-templates/templates/game-design-document.md`
- `plugins/AGDA/docs/reference-templates/templates/architecture-traceability.md`

## Method

Review the selected design doc as a separate pass from authoring. Re-read the design doc, epic reference row, and architecture baseline from disk. Do not rely on memory of the draft.

Check:

- The design doc intent is clear and bounded.
- Scope, constraints, dependencies, and non-goals are consistent.
- Validation shape is testable.
- The design doc does not contradict the approved system map or architecture baseline.
- Any new or changed architecture dependency is surfaced as a blocker or explicit follow-up.
- The design doc is ready for story shaping, or it still needs architecture work first.

If the design needs revision, revise the design doc directly and rerun the review.

If the design is approved but the epic still needs an architecture check, route to `technical-architecture`.

If the design is approved and no architecture follow-up is needed, route to `story-shaping`.

## Output

Update the design doc, epic reference row, and backlog/status only as needed to record the review result and next step.

## Stage Exit

If the design is approved and architecture work is still needed:

```text
Recommended next skill: technical-architecture
```

If the design is approved and no architecture work is needed:

```text
Recommended next skill: story-shaping
```

If the design still needs revision:

```text
Recommended next skill: system-design
```

