# Reference Map

AGDA uses a compact conception spine and integrates selected local reference assets for concept depth, systems mapping, technical architecture, ADR Creation, handoff, and lean request-led production.

## Source Inventory

Module agents copied: **5**

- `src/agents/gds-agent-game-architect/`
- `src/agents/gds-agent-game-designer/`
- `src/agents/gds-agent-game-dev/`
- `src/agents/gds-agent-game-solo-dev/`
- `src/agents/gds-agent-tech-writer/`

Preproduction workflow skills copied: **3**

- `src/workflows/1-preproduction/gds-brainstorm-game/`
- `src/workflows/1-preproduction/gds-create-game-brief/`
- `src/workflows/1-preproduction/research/gds-domain-research/`

Preproduction support workflows copied:

- `src/workflows/1-preproduction/research/workflow-market-research.md`
- `src/workflows/1-preproduction/research/workflow-technical-research.md`
- shared research step files and templates under `src/workflows/1-preproduction/research/`

## Primary New-Game Flow

Use the compact game brief sequence as the conception spine.

Conception stages:

1. Initialization / resume
2. Vision
3. Player and experience fit
4. Fundamentals
5. Scope
6. References
7. Content and production
8. Core loop design
9. MDA and player motivation
10. Pillars and anti-pillars
11. Scope feasibility and MVP
12. Final review and next action

## Optional Path

Use `gds-brainstorm-game` only when the user wants ideation before committing to a brief.

## Research Path

Research workflows are copied for reference material, but they should run only when explicitly requested.

## Integrated Reference Points

Integrated points:

1. Short project stage detection from `/start` and `/project-stage-detect`.
2. Core loop, pillars/anti-pillars, player validation, and scope/feasibility from `/brainstorm` and `game-concept.md`.
3. Systems decomposition from `/map-systems` and `systems-index.md`.
4. Technical architecture from `/create-architecture`, `/architecture-review`, and traceability docs.
5. ADR Creation from `/architecture-decision` and ADR templates.
6. Final production handoff from readiness gates and review workflow docs.
7. Production planning from milestone/backlog references and compact request/task/review discipline.
8. Production routing inside the single status-check skill from current stage, active epic/story/task, backlog statuses, review evidence, and next executable item.
9. Requests Intake from a human request, classification, epic update/creation when needed, and routing into the production lane.
10. Production design routing through the existing `system-design` / `system-design-review` loop for the next unfinished epic.
11. Scoped production ADRs only when the active epic names a significant hard-to-reverse or cross-system decision.
12. Epic shaping from one shaped epic into bounded story and task breakdown.
13. Story execution coordinates subagents across ready task sections; task execution remains the single-task worker contract with deterministic gates, Code Review Gate, Defined -> Connected -> Reachable validation, task review, task-local clean/sweep, and status updates.
14. Epic review from completed stories, build/test evidence, playtest feedback, backlog routing, and next-epic implications.
15. Optional bug-fix session lane from reproduction, severity, fix, validation, review, and backlog/status updates.
16. Release management from completed work, semantic versioning, and player-facing release notes.
19. Godot production implementation references from GD Agentic Skills, used only as targeted work/task-level source material during production.

Copied readiness skill source:

- `.claude/skills/start/`
- `.claude/skills/project-stage-detect/`
- `.claude/skills/brainstorm/`
- `.claude/skills/map-systems/`
- `.claude/skills/design-system/`
- `.claude/skills/design-review/`
- `.claude/skills/review-all-gdds/`
- `.claude/skills/create-architecture/`
- `.claude/skills/architecture-decision/`
- `.claude/skills/architecture-review/`
- `.claude/skills/gate-check/`

Copied docs/templates:

- `game-concept.md`
- `game-pillars.md`
- `systems-index.md`
- `game-design-document.md`
- `technical-design-document.md`
- `architecture-decision-record.md`
- `architecture-traceability.md`
- `prototype-report.md`
- `vertical-slice-report.md`
- `project-stage-report.md`
- `quick-start.md`
- `directory-structure.md`
- `director-gates.md`
- `review-workflow.md`

Copied reference skill mirrors that are not exposed as plugin skills:

```text
plugins/AGDA/docs/reference-skills/reference-game-brief/
plugins/AGDA/docs/reference-skills/reference-readiness/
```

External production reference that is not exposed as a plugin skill:

```text
plugins/AGDA/docs/reference-skills/reference-godot-production.md
plugins/AGDA/docs/reference-sources/gd-agentic-skills/
```

This reference vendors `thedivergentai/gd-agentic-skills` under docs/reference sources and is used only for Godot implementation routing. This is direct bundled source material, not just inspiration. These source skills are not AGDA plugin skills and should not be surfaced. AGDA should consult only the smallest relevant source skill(s) for the current task.

Local flow templates that are not exposed as plugin skills:

```text
plugins/AGDA/docs/templates/
```

## Production Flow

Production is request-led and task-led.

| Stage | Purpose | Input | Output | Skill |
| --- | --- | --- | --- | --- |
| Production Planning | Convert approved preproduction into milestones, backlog routing, build order, and epic docs only when the work needs 2+ stories. Do not create stories or tasks for single-item work. | `preproduction/production-handoff.md`, `preproduction/systems.md`, architecture read-first contracts, ADR index | `production/plan.md`, `production/backlog.md`, `production/status.md`, `production/epics/EPIC-###.md` | `production-planning` |
| Status Check | Resume production by finding the current stage, active epic/story/task, and next executable item. | plan, backlog, status, epic/review files, release notes | routing report with next item | `status-check` |
| Requests Intake | Classify a human request and create or update an epic only when the work needs 2+ stories. | human request, plan, backlog, status, epic docs | updated plan/backlog/status/epic or direct route to the next stage | `requests-intake` |
| Production Design Loop | Update/review the selected epic's design notes and return to intake or shaping with any architecture/ADR blocker recorded. | production request, active epic, system map, architecture baseline, status | approved design delta and optional blocker | `system-design` / `system-design-review` |
| Scoped Production ADR | Capture a significant production decision only when explicitly required by design review or the active epic. | design review blocker, active epic, architecture contracts | accepted scoped ADR and cleared blocker | `adr-creation` |
| Epic Shaping | Split a shaped epic into bounded story/task breakdown in the epic document when the work needs 2+ stories. | plan, backlog, status, epic row/document, design/architecture inputs when needed | `production/epics/EPIC-###.md`, updated backlog/status | `story-shaping` |
| Work Execution | Spawn worker subagents for ready task sections in the active story, pass `task-execution` to each worker, integrate results, enforce deterministic gates plus the code review gate, and continue until the story is ready for review. For Godot projects, consult only relevant GD Agentic Skills source references. Approved work must commit when git is available. | active story, task sections, architecture contracts, touched design/ADR bodies only when needed, targeted engine references when applicable, `task-execution` worker contract | code changes, test/build evidence, story reviews, updated backlog/status, commit hashes | `work-execution` |
| Task Execution | Worker contract for exactly one assigned task section. Used by `work-execution` subagents or directly for standalone tasks. | one task section, parent story if any, scoped design/architecture references | one task implementation, code review gate, one task review, task status update, optional commit hash | `task-execution` |
| Epic Review | Close the epic, including playtest or operator feedback, backlog routing, and engine-specific evidence checks where applicable. | completed tasks, build/test evidence, task reviews, playable build/playtest notes | `production/reviews/[WORK-ID]-review.md`, updated backlog/status/epic | `work-review` |
| Bug Fix Session | Optional lane for standalone bug items. The session spawns one bugfix worker per bug and approved fixes must commit when git is available. | standalone bug files, reproduction context, build/test evidence | fixes, validation evidence, optional bug files, updated backlog/status, commit hash | `bug-fix-session` |
| Release Management | Compare the latest release to completed work, archive the current backlog as the versioned backlog, decide the next semantic version, and write player-facing release notes. | latest `production/releases/v*.md`, backlog, reviews, user request for major bump if any | `production/releases/vX.Y.Z.md`, `production/releases/vX.Y.Z-backlog.md`, fresh `production/backlog.md` | `manage-release` |

`production/backlog.md` is the single source of production routing. Full epic docs live in `production/epics/EPIC-###.md`. Production planning creates epics only when the work needs 2+ stories. Requests Intake is for human requests once the backlog needs a new item. It creates or updates epics only when work needs 2+ stories; single stories, standalone tasks, and bugs can stay standalone. Design-affecting Requests Intake uses the existing system design/review loop, then returns to the production lane for any architecture check or epic shaping. Full technical architecture remains a preproduction baseline step, while production ADRs are scoped exceptions. Epic shaping creates story/task breakdown inside the epic document only when an epic is justified; work execution coordinates worker subagents across all ready task sections in the active story, passes the task-execution worker contract to each subagent, and stops when the story is ready for review.

## License

Brief workflow source is copied under the MIT license included at:

```text
plugins/AGDA/LICENSE-AGDA-BRIEF
```

Readiness workflow source is copied under the MIT license included at:

```text
plugins/AGDA/LICENSE-AGDA-READINESS
```

GD Agentic Skills source is directly vendored under the LGPL-3.0 license included at:

```text
plugins/AGDA/LICENSE-AGDA-GODOT-REFERENCE
plugins/AGDA/docs/reference-sources/gd-agentic-skills/LICENSE
```

