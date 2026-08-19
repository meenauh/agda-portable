---
name: production-planning
description: Create the lean AGDA production plan, backlog routing, and production status from an approved production handoff.
---

# AGDA: Production Planning

Use this skill after `preproduction/production-handoff.md` passes.

It creates or updates:

```text
production/plan.md
production/backlog.md
production/status.md
production/epics/EPIC-###.md
```

Do not create story or task breakdown in this skill. Production planning seeds epics only for work that needs 2+ stories; single stories, standalone tasks, and bugs stay out of the epic lane.

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Source Rules

Use local project artifacts first:

- `preproduction/production-handoff.md`
- `preproduction/systems.md`
- `preproduction/architecture/technical.md`
- `preproduction/architecture/reviews.md`

Use local templates:

- `plugins/AGDA/docs/templates/production-plan.md`
- `plugins/AGDA/docs/templates/production-backlog.md`
- `plugins/AGDA/docs/templates/production-status.md`
- `plugins/AGDA/docs/templates/epic.md`

Use reference ideas only as patterns:

- milestones from the handoff and architecture gates
- optional epics from systems map and architecture
- acceptance criteria that are observable or testable
- dependency-safe implementation order

## Method

1. Verify the production handoff exists and does not list open blockers.
2. Read the systems map, architecture read-first contracts, and ADR index. Open any additional source material only when needed to write acceptance criteria or dependencies for an epic.
3. Create milestones with concrete exit criteria.
4. Create optional epics only when the work is expected to split into 2+ stories. Do not force an epic for a single story, a standalone task, or a bug.
5. Order epics by dependencies. Do not allow circular dependency language.
6. Create the initial backlog from production goals as epic rows only. Do not create Milestone, Type, or Depends On columns: milestones and dependencies belong in `production/plan.md` and epic documents, and the ID identifies the item type. Put detailed risks into epic docs when they require action; do not keep duplicate detailed risk prose in the plan.
7. Create one epic document per epic at `production/epics/EPIC-###.md`. The backlog row is only an index.
8. Do not create story or task rows or documents in production planning. `story-shaping` is the only skill that creates stories and tasks.
9. Allocate epic IDs incrementally:
   - scan existing `EPIC-###` IDs in `production/backlog.md`, `production/plan.md`, and `production/epics/*.md`;
   - if no ID of that type exists yet, start at `000`;
   - otherwise use the highest existing number for that type plus one;
   - do not fill gaps or restart numbering by milestone, epic, or work group;
   - preserve three-digit padding until the sequence exceeds `999`.
10. Keep epics player-facing or operator-facing:
   - feature epics describe player-visible outcomes;
   - technical and tooling epics describe operator/developer outcomes;
   - every story and task may be standalone if it is single-item work; use an epic only when the work needs 2+ stories.
11. Ensure M0 Technical Baseline includes repository hygiene as an epic only if the setup work needs 2+ stories; otherwise keep it as a standalone story or task:
   - create or update an epic such as `EPIC-000 Project Setup` only when warranted;
   - validation for the work must include `git status --short` and evidence that generated/cache/source folders are ignored when applicable.
12. Create/update `production/status.md` as a one-screen routing pointer with only current stage, active epic/story/task, next executable item, blockers, latest evidence pointer, and recommended next action.
13. Set the recommended next skill to `system-design` for the first unfinished epic created by production planning. Use `requests-intake` only later when the human wants to add a new feature, improvement, bugfix, or other work that was not already seeded by production planning.

## Backlog Rules

`production/backlog.md` is the single source of production routing.

Backlog items can be epics, standalone stories, standalone tasks, or bugs.

Bugs are standalone. Tuning, polish, design changes, and deferred ideas can stay standalone when they are small. Use epics only when work needs 2+ stories. Story and task breakdown live only in the epic document when an epic exists. Production planning creates initial epics only for multi-story work. Requests Intake creates or updates epics only when needed. System design expands the epic into design notes. Story shaping expands the epic into stories and tasks. Stories and tasks may be standalone when they are single-item work.

## Output Requirements

`production/plan.md` must include:

- source artifacts
- production goal
- milestones with exit criteria
- optional epics with source systems and architecture
- dependency-safe build order
- production gates
- strategic risks only when they are not yet actionable backlog work

`production/backlog.md` must include:

- an epics section with epic IDs, purpose, exit criteria, source references, and epic doc paths
- an ID allocation note: IDs are global per type and always use the highest existing number plus one

Full epic acceptance criteria and validation/evidence requirements live in `production/epics/EPIC-###.md`.

`production/status.md` must include:

- current stage
- active epic/story/task
- next executable item
- blockers
- latest evidence pointer

Keep `production/status.md` to one screen. Do not copy full acceptance criteria, validation instructions, task rationale, or evidence logs into status.

## Stage Exit

End with:

```text
Recommended next skill: system-design
```

