# Production Backlog

This is the single source of production routing. It keeps epics only for work that needs 2+ stories; story and task breakdown live in the matching epic document when one exists.

## Status Values

`Ready`, `Planned`, `In Progress`, `Review`, `Done`, `Blocked`, `Deferred`

## Epic Status Values

`Planned`, `Active`, `Done`, `Blocked`, `Deferred`

## ID Allocation

Use global incremental IDs per type:

- Next epic ID: scan all `EPIC-###` IDs, take the highest number, add 1.
- Next story ID: scan all `STORY-###` IDs in `production/epics/*.md`, take the highest number, add 1.
- Next task ID: scan all `TASK-###` IDs in `production/epics/*.md`, take the highest number, add 1.

If no ID of that type exists yet, start at `000`. Do not fill gaps. Do not restart task numbers per work item. Preserve three-digit padding until the sequence exceeds `999`.

## Epics

Epics are the backlog items for multi-story work. They are not directly executable.

The table has no `Type` or `Depends On` column: the ID identifies the item type, while dependencies live in `production/plan.md` and the epic document.

| Epic ID | Epic | Epic Doc | Status | Purpose | Exit Criteria | Source | Planned Volume | Done Volume |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| EPIC-000 | Project Setup | `production/epics/EPIC-000.md` | Planned | Establish a runnable, versioned project baseline. | The project can be built or opened, source control is initialized, and generated/cache artifacts are ignored. | Production planning | 0 | 0 |

## Routing Notes

- Bugs, tuning, polish, design changes, and deferred ideas only need an epic when they need 2+ stories.
- Design changes must reference the affected systems and architecture docs and cannot be implemented until those docs are updated when the change affects approved design.
- Story and task breakdown live in the epic document, not in the backlog.
- Full epic acceptance criteria, story breakdown, task breakdown, validation requirements, constraints, non-goals, and test plans live in `production/epics/EPIC-###.md`, not in this backlog table.
- `Planned Volume` and `Done Volume` are rollups of leaf estimates from the epic doc. Use them to watch the 100-point release cap.

