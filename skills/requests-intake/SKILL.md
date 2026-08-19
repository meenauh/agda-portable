---
name: requests-intake
description: Classify a request, update or create the epic, and route production work to the next unfinished epic stage.
---

# AGDA: Requests Intake

Use this skill when a human brings a new request and the backlog has no open epics. It is the entrypoint for multi-story work, standalone stories, standalone tasks, bug reports, and improvement requests once production exists and the current epic queue is closed.

It creates or updates:

```text
production/plan.md
production/backlog.md
production/status.md
production/epics/EPIC-###.md
production/bugs/[BUG-ID].md
```

## Git Worktree Boundary

Before creating or editing any production artifact, allocate the request's epic, story, task, or bug ID, then create one dedicated `<host>/<ITEM-ID>-<slug>` worktree branch from `develop`; use the host or team prefix configured for the project. Immediately copy `develop/.env` into the new worktree before dependency installation or any work. Record its path and branch in `production/status.md`. All downstream production skills for that item must resume in this worktree; never write request artifacts in the primary `develop` checkout. Keep this branch through design, shaping, execution, and review. Merge it into `develop` only when its final approval gate succeeds. If the project has no git repository, `develop` is unavailable, or its `.env` file cannot be copied, stop before writing and route the repository setup blocker.

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Source Rules

Read local project files first:

- `production/plan.md`
- `production/backlog.md`
- `production/status.md`
- relevant `production/epics/EPIC-###.md` files
- relevant `production/reviews/*.md` files
- `preproduction/systems.md` only when a request changes the approved system map or baseline architecture
- `preproduction/architecture/technical.md` only to check existing contracts or explicit architecture/ADR blockers

Use the production design loop:

- `plugins/AGDA/skills/system-design/SKILL.md`
- `plugins/AGDA/skills/system-design-review/SKILL.md`
- `plugins/AGDA/skills/technical-architecture/SKILL.md`

Use the template:

- `plugins/AGDA/docs/templates/epic.md`

## Method

### Pass 1: Classify And Route

1. Read the human request and classify it as one of:
   - new feature
   - bugfix
   - improvement
2. Decide whether the request changes the approved system map or baseline architecture.
3. Allocate the request item ID, create its dedicated worktree branch, copy `develop/.env` into it, and record it in status before writing any request artifact.
4. If the request needs 2+ stories, create or update the relevant epic and route it into the production design path: `system-design`, then `system-design-review`, then `technical-architecture` if needed.
5. If the request is only 1 story, keep it standalone and skip epic creation.
6. If the request is only 1 task with no user impact, keep it standalone and skip story creation.
7. If the request is a bugfix, keep it standalone and hand off to `bug-fix-session`.
8. If the request changes the approved system map or baseline architecture, route back to preproduction first. Otherwise stay in production.

### Pass 2: Resume After Design Approval

Run this only after `system-design-review` has approved the selected epic design.

7. Read the latest design review result and affected epic rows.
8. Decide whether the epic needs architecture follow-up:
   - New feature: attach to the active epic or create a new one if one is broad enough to need decomposition.
   - Small new feature: keep it standalone unless it clearly needs an epic.
   - Improvement: attach to an existing relevant epic when one clearly applies; otherwise keep it standalone unless the improvement is broad enough to need decomposition.
   - Bugfix: attach to an existing relevant epic when one clearly applies; otherwise keep it standalone unless the bug set is broad enough to need shared decomposition.
9. When creating a new epic, allocate the ID globally by scanning existing IDs and using the highest number plus one:
   - next epic: `EPIC-000` if none exist, otherwise max `EPIC-###` + 1;
   - do not fill gaps or restart numbering per epic, milestone, or request.
10. If the request needs 2+ stories, create or update the epic in `production/plan.md`, `production/backlog.md`, and `production/epics/EPIC-###.md`.
11. If the design review names a hard-to-reverse, cross-system, persistence, engine/stack, save/state, networking, content pipeline, platform, tooling, or architecture-boundary decision, record an architecture/ADR follow-up requirement on the created or updated epic before story shaping.
12. Route to `technical-architecture` for the feature/improvement architecture and ADR check if the request needs one. If the check finds a scoped decision, route to `adr-creation` for that decision. If the blocker is broader than one decision and cannot be resolved by a scoped ADR, keep it in `technical-architecture` for that blocker only.
13. If no architecture/ADR blocker exists after the check, continue to `story-shaping` only when an epic exists.
14. Keep the request sized correctly. Do not force an epic or story breakdown when the work is small enough to stay standalone.
15. Update `production/status.md` with the current request, any approved epic, standalone story, standalone task, or standalone bug item, any architecture/ADR blocker, and the next required skill.

## Routing Rules

- New feature:
  - route to `system-design`
  - then route to `system-design-review`
  - create or update an epic only when the request needs 2+ stories
  - run the architecture/ADR check if the epic needs it
  - if no architecture/ADR blocker exists and an epic exists, end with `story-shaping`
  - if a scoped production ADR is required, end with `adr-creation`
- Improvement:
  - route to `system-design`
  - then route to `system-design-review` to update the epic design notes
  - after approval, create or update the epic only if one is needed
  - run the architecture/ADR check if the epic needs it
  - if no architecture/ADR blocker exists, end with `story-shaping`
  - if a scoped production ADR is required, end with `adr-creation`
- Bugfix:
  - if no design change is required, keep the bug standalone and end with `bug-fix-session`
  - if design changes are required, route through `system-design` first, then resume intake and keep the bug standalone before ending with `bug-fix-session`
  - if the design review finds a significant architecture decision, record the blocker and end with `adr-creation`
  - if a concrete child bug task already exists, end with `bug-fix-session`

Run `technical-architecture` in check mode for every feature and meaningful improvement when the request needs an architecture decision. Use the result to decide whether the request needs `adr-creation`, a broader architecture update, or no further architecture work.

## Output Requirements

The intake output must be compact:

- request classification
- design required yes/no
- affected epic
- architecture/ADR blocker yes/no
- backlog action
- next skill

Do not create tasks. Do not ask the human to approve every small decision; only stop when a design decision cannot be inferred responsibly.

## Stage Exit

If feature design is required and not yet approved:

```text
Recommended next skill: system-design
```

If system design is complete and the architecture/ADR check has not yet been run:

```text
Recommended next skill: technical-architecture
```

If design is approved and the epic has been shaped:

```text
Recommended next skill: story-shaping
```

If design is approved but a scoped production ADR is required:

```text
Recommended next skill: adr-creation
```

If design is approved but the blocker requires an architecture update broader than one ADR:

```text
Recommended next skill: technical-architecture
```

If this is a bugfix with no design change:

```text
Recommended next skill: bug-fix-session
```

If this is a feature or improvement and the design path has just started:

```text
Recommended next skill: system-design
```

If the backlog still has an open epic, do not recommend `requests-intake`; recommend `system-design` for the next unfinished epic instead.

