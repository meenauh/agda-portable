---
name: production-handoff
description: Validate preproduction gates and create the production handoff.
---

# AGDA: Production Handoff

Use this skill after conception, systems mapping, technical architecture, and required ADR creation.

It creates or updates:

```text
preproduction/production-handoff.md
```

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Source Rules

Use the local reference material as the authority for readiness checks:

- `plugins/AGDA/docs/reference-skills/reference-readiness/gate-check/REFERENCE_SKILL.md`
- `plugins/AGDA/docs/reference-templates/director-gates.md`
- `plugins/AGDA/docs/reference-templates/review-workflow.md`

Use the local template:

- `plugins/AGDA/docs/templates/production-handoff.md`

## Required Inputs

For a new game:

- `preproduction/design.md`
- `preproduction/systems.md`
- reviewed and approved `preproduction/architecture/technical.md`
- reviewed and accepted required `preproduction/architecture/adrs/[NNNN]-[slug].md` files or explicit reviewed deferrals
- technical and ADR review evidence in `preproduction/architecture/reviews.md`

For an existing project:

- `preproduction/project-context.md`
- `preproduction/systems.md`
- `preproduction/architecture/technical.md`

## Gate Rules

Do not fake completeness. If an item is missing, report it as missing and name the next skill to run.

New game handoff requires:

- player fantasy
- design pillars and anti-pillars
- core loop
- intended player experience
- MVP and non-goals
- scope and constraints
- main systems and dependencies
- systems priority and topological design order
- no circular dependencies in `preproduction/systems.md`
- technical architecture with architecture review evidence in `preproduction/architecture/reviews.md`
- required ADRs with ADR review evidence in `preproduction/architecture/reviews.md` or explicit reviewed deferrals

The handoff must fail if any artifact is only self-reviewed, lacks matching review evidence, or uses an approved/accepted status without matching review evidence. Technical and ADR reviews belong in `preproduction/architecture/reviews.md`, never in `preproduction/architecture/adrs/`.

Existing project handoff requires:

- repo type and engine/stack
- build/test/lint/package commands when discoverable
- existing systems and boundaries
- technical risks
- current architecture summary

## Output

Create a concise `production-handoff.md` with:

- project type
- MVP/current target
- core systems
- design readiness
- technical architecture readiness
- required ADR status
- technical review evidence
- production quality gates
- out of scope
- open blockers

## Stage Exit

When the handoff gate passes, end the response with:

```text
Recommended next skill: production-planning
```

When the handoff gate fails, end with the missing stage's visible skill name, for example:

```text
Recommended next skill: technical-architecture
```

