---
name: story-shaping
description: Split an approved epic into story and task breakdown in the epic document.
---

# AGDA: Story Shaping

Use this skill after `production-planning` or `requests-intake` has created or updated an epic that needs 2+ stories and is ready to be decomposed into stories and tasks.

It creates or updates:

```text
production/epics/EPIC-###.md
production/backlog.md
production/status.md
```

## Git Worktree Boundary

Run only in the active request worktree recorded by `requests-intake` in `production/status.md`. Write no production artifact from the primary `develop` checkout. Keep the request branch unmerged until final work approval.

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Source Rules

Read:

- `production/plan.md`
- `production/backlog.md`
- `production/status.md`
- `plugins/AGDA/docs/backlog-estimation.md`
- the matching epic row in `production/backlog.md`
- the epic document at `production/epics/EPIC-###.md`
- `preproduction/systems.md`
- `preproduction/architecture/technical.md` read-first contracts when the epic touches implementation boundaries
- relevant ADRs only when the epic depends on them

Use the template:

- `plugins/AGDA/docs/templates/epic.md`

## Method

1. Identify the parent epic and confirm it is ready to be decomposed.
2. Read `plugins/AGDA/docs/backlog-estimation.md` and use its fixed scale and rollup rules.
3. Read the epic acceptance criteria, validation requirements, constraints, non-goals, and any linked design/architecture inputs.
4. For an existing backlog, inspect the current story/task sections in the epic doc and assign or revise leaf estimates before adding new breakdown.
5. Split the epic into the smallest practical bounded stories.
6. Split each story into the smallest practical bounded tasks that can be executed and reviewed independently.
7. Estimate only leaf work:
   - tasks and bugs get direct volume values;
   - standalone stories get a direct volume value;
   - epics get the sum of their leaf children;
   - if any leaf item is larger than `13`, split it.
8. Allocate story and task IDs globally:
   - scan every `STORY-###` and `TASK-###` in `production/backlog.md` and `production/epics/*.md`;
   - if no ID of that type exists yet, start at `000`;
   - otherwise assign each new ID the highest existing number plus one;
   - increment by one for each additional story or task in this shaping run;
   - do not fill gaps and do not restart numbering per epic.
9. Update the epic document with compact story and task tables, full story/task details, and `Planned Volume` / `Done Volume` rollups.
10. Update the parent epic row in `production/backlog.md` with the epic status and epic doc pointer only; do not add story or task rows.
11. Update `production/status.md` to point at the next executable story or task and its epic document, plus `Scope loaded: X/100` and `Completeness: Y/100` when the numbers are available.

## Shaping Rules

- Each story should describe a coherent player-facing or operator-facing outcome.
- Each task should be small enough to finish, validate, and review in a single execution pass.
- Use the fixed volume scale from `plugins/AGDA/docs/backlog-estimation.md`: `1, 2, 3, 5, 8, 13`.
- Count leaf work only. Do not count the same work at story, task, and epic level.
- If a piece of work is larger than `13`, split it before assigning volume.
- A task may touch multiple files only when they are directly required by the same bounded change.
- If a story cannot be split into bounded tasks without guesswork, refine the story before creating task sections.
- Do not create separate story or task documents. The epic document is the source of truth.
- Do not create separate design documents. If decomposition needs design notes, add them to the referenced production design doc and keep the epic as a reference index.

## Output Requirements

The backlog must show:

- epic rows only
- a pointer from each epic row to `production/epics/EPIC-###.md`
- clear evidence pointers for the epic

Each `production/epics/EPIC-###.md` must contain:

- epic summary
- story breakdown
- task breakdown
- planned and done volume rollups
- acceptance criteria
- validation requirements
- constraints
- non-goals
- task review guidance

Do not invent unrelated backlog work here. Do not create epics outside the current scope. Do not create task documents.

## Stage Exit

If stories and tasks are ready for implementation:

```text
Recommended next skill: work-execution
```

If the epic still needs request or design work first:

```text
Recommended next skill: requests-intake
```

