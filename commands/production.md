# Production Flow

This file documents the AGDA production flow for maintainers. Codex currently surfaces production through skills, not custom slash commands.

## Flow

| Stage | Description / Purpose | Input | Output | Skill |
| --- | --- | --- | --- | --- |
| Production Planning | Convert approved preproduction into milestones, backlog routing, build order, and initial epic docs only when the work needs 2+ stories. Do not create stories or tasks for single-item work. | `preproduction/production-handoff.md`, `preproduction/systems.md`, `preproduction/architecture/technical.md`, ADRs | `production/plan.md`, `production/backlog.md`, `production/status.md`, `production/epics/EPIC-###.md` | `production-planning` |
| Status Check | Resume production by finding the current stage, active epic/story/task, and next executable item. | `production/plan.md`, `production/backlog.md`, `production/status.md`, epic/review files, release notes | Routing report with next item and recommended skill | `status-check` |
| Requests Intake | Classify a human request as new feature, improvement, task, or bugfix; create or update an epic only when the work needs 2+ stories, otherwise keep it standalone. | human request, plan, backlog, status, epic docs | updated plan/backlog/status/epic or direct route to the next stage | `requests-intake` |
| Production Design Loop | For the next unfinished epic, update the epic design notes and review them before story shaping. | production request, active epic, system map, architecture baseline, status | approved epic design delta and optional architecture/ADR blocker | `system-design` / `system-design-review` |
| Scoped Production ADR | Only when the active epic names a significant hard-to-reverse or cross-system decision. Do not rerun full architecture for ordinary epics. | approved epic design delta, active epic blocker, architecture contracts | accepted scoped ADR and cleared blocker | `adr-creation` |
| Epic Shaping | Split an epic that needs 2+ stories into bounded story/task breakdown in the epic document. | `production/plan.md`, `production/backlog.md`, `production/status.md`, parent epic, design/architecture inputs when needed | `production/epics/EPIC-###.md`, updated backlog/status | `story-shaping` |
| Work Execution | Spawn worker subagents for ready task sections in the active story, pass `task-execution` to each worker, integrate results, enforce deterministic gates plus the code review gate, and continue until the story is ready for review. | Active story, task sections, architecture contracts, touched design/ADR bodies only when needed, `task-execution` worker contract | Code changes, build/test evidence, `production/reviews/[STORY-ID]-review.md`, updated backlog/status, commit hashes | `work-execution` |
| Task Execution | Worker contract for exactly one assigned task section. Used by `work-execution` subagents or directly for standalone tasks. | One task section, parent story if any, scoped design/architecture references | One task implementation, code review gate, one task review, task status update, optional commit hash | `task-execution` |
| Epic Review | Close the epic as a playable or operator-verifiable increment. Include human feedback and route follow-up work into the backlog; if any epic remains open, route to the next epic's design loop instead of Requests Intake. | Completed stories, task reviews, build/test evidence, playable build or operator notes | `production/reviews/[WORK-ID]-review.md`, updated backlog/status/epic | `work-review` |
| Bug Fix Session | Optional lane for one or more concrete bug items. The session spawns one bugfix worker per bug and keeps bug work prioritized against feature work. Approved fixes commit with `fix([BUG-ID])`. | Bug task sections or standalone bug files, reproduction context, build/test evidence | Fixes, validation evidence, optional `production/bugs/[BUG-ID].md`, updated backlog/status, commit hash | `bug-fix-session` |
| Release Management | Compare the latest release to completed work, archive the current backlog as the versioned backlog, decide the next semantic version, and write player-facing release notes. | Latest release notes, backlog, reviews, user request for major bump if any | `production/releases/vX.Y.Z.md`, `production/releases/vX.Y.Z-backlog.md`, fresh `production/backlog.md` | `manage-release` |

## Single Backlog Rule

`production/backlog.md` is the single source of production routing, but it is not where full epic/story/task breakdown lives.

Epics are only created when the work needs 2+ stories.

Bugs are standalone. A single story is standalone. A single internal task can also be standalone when it has no user impact. Production planning creates epics only for multi-story work. Requests Intake is the human entrypoint once the backlog needs a new item. Story shaping creates story/task breakdown inside the epic document only when an epic is justified. Tasks may be standalone when they do not need a story.

## Gate Rules

- No production plan without a passed production handoff.
- No epic without a full `production/epics/EPIC-###.md` document containing goal, acceptance criteria, and validation notes.
- No task without a full task section containing acceptance criteria and validation notes, unless it is a standalone internal task.
- No task without a parent story, unless it is a standalone internal task.
- No epic unless the work needs 2+ stories.
- No task closes without acceptance evidence, deterministic build/test evidence, review evidence, Defined -> Connected -> Reachable evidence, and task-local clean/sweep evidence.
- No task closes with unresolved `Critical` or unresolved `Important` code review findings.
- No work execution run stops for user approval between ready tasks in the active story; it stops when the story is ready for `work-review`, blocked, or requires design/intake.
- No epic closes without an epic review.
- No bug closes without reproduction or a clear validation guard.
- No design change bypasses the approved system map or architecture baseline.
- No production Requests Intake skips the technical-architecture check when an epic or standalone story needs it.
- No production ADR is created unless the active epic, status snapshot, or design review explicitly names a significant architecture decision.
- No scoped production ADR blocks story shaping after it is accepted and the epic/status blocker is cleared.

