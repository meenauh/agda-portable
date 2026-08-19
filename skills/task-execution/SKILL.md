---
name: task-execution
description: Execute exactly one AGDA production task as a focused worker session with scope locking, deterministic gates, review, fix loop, clean/sweep, evidence, and backlog/status updates.
---

# AGDA: Task Execution

Use this skill when production has a shaped task that is ready to implement, whether it belongs to a story or stands alone.

This skill executes exactly one production task section per invocation. It is the worker contract that `work-execution` passes to subagents. Do not continue into the next task in the same session.

It updates:

```text
production/backlog.md
production/status.md
production/epics/EPIC-###.md
production/reviews/[ITEM-ID]-review.md
```

It may also change project code and tests. Approved task work must end in a git commit when the project has a git repository.

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Git Worktree Rules

For a git project, all task writes happen in the active request worktree created by `requests-intake`; never implement, edit evidence, or commit from the primary `develop` checkout. Record that worktree path and branch in review evidence. When creating a child task worktree, immediately copy `develop/.env` into it before dependency installation or execution. A coordinator may use it only when it branches from this active request branch and merges back to it—never directly to `develop`.

## Source Rules

Read:

- `production/backlog.md`
- `production/status.md`
- only the matching task section in the epic document, standalone task record, or direct task file, including parent story when any, dependencies, task anchor path, and evidence pointer
- the matching task section at `production/epics/EPIC-###.md` when it exists, including acceptance criteria, validation requirements, constraints, non-goals, and test plan
- the parent story section and epic row when they exist
- read-first contracts in `preproduction/architecture/technical.md` only if they exist or are named by the backlog row
- relevant architecture and ADR references only when referenced by the matching backlog row, matching task section, parent story, or required to resolve implementation details
- any existing review or bug file for the selected item
- if the project uses Godot: `plugins/AGDA/docs/reference-skills/reference-godot-production.md`

Do not read the whole `production/plan.md` or every full architecture/ADR body during normal task execution. Use `production/status.md`, the matching backlog row, the parent story, and the matching task section as the working set. Use architecture read-first contracts as accelerators when present, not as mandatory inputs. Consult `production/plan.md` or full design/ADR bodies only when the selected task cannot be interpreted from the row-driven working set.

Do not run broad memory searches for ordinary AGDA task execution. Local project files are the authority. Use memory only when the user explicitly asks for prior session context or local files are insufficient to route the project.

Use the template:

- `plugins/AGDA/docs/templates/task-review.md`

## Task Selection

Select one item only:

1. If `production/status.md` names an active item with status `In Progress` or `Review`, resume that item.
2. Otherwise, select the first backlog task with status `Planned`, `Ready`, or `Blocked` where the blocker has been cleared.
3. If no selected task is executable, do not invent work. Recommend `work-review` if the parent story is complete, otherwise update status with the blocker.

Immediately set the current session title to the selected task's exact ID and title when the active host supports it, for example `TASK-074 Image preload`. Do this before preflight or implementation; otherwise skip this optional presentation action.

## Required Preflight

Before implementation:

- Confirm the item exists in `production/backlog.md`.
- Confirm the item is a task section and has a parent story assigned, or is explicitly standalone.
- Confirm the task section exists in the epic document or standalone task record.
- Confirm the parent story section exists when the task is not standalone.
- Confirm acceptance criteria in the task section are executable: test passes, observable behavior, or state/file condition.
- Confirm validation/evidence requirements in the task section are explicit.
- Confirm dependencies are `Done` or not required.
- Confirm the work does not require changing approved systems, architecture, or ADRs first.
- Record the current git state or changed-file baseline in the review file.
- Confirm the current checkout is the active request worktree or an allowed child of it, and its branch is not `develop`.
- If `.git/` is missing and this is a scaffold, technical baseline, or repository hygiene story, initialize git and create/update `.gitignore` before implementation evidence is recorded.
- If `.git/` is missing and the selected task is not allowed to set up repository hygiene, stop and add/update a P0 backlog item for repository setup.
- If the project uses Godot, identify the one or two relevant GD Agentic Skills source references from `reference-godot-production.md`. Do not load the whole source library or full micro-skills by default.

If any preflight check fails, do not implement. Update `production/status.md` and recommend the required skill.

## Engine Reference Rules

For Godot projects:

- Use `reference-godot-production.md` as a routing table, not as a new workflow stage.
- Consult only the source skill(s) that match the selected task domain.
- Within a source skill, read only the relevant implementation and "NEVER" sections for the selected task. Do not read the whole micro-skill when a narrower section answers the question.
- Apply relevant implementation patterns and "NEVER" rules to changed files and direct consumers.
- If a source rule suggests broader cleanup, architecture migration, export setup, or tooling outside the task scope, add/update a backlog item instead of expanding the current task.
- Record consulted source skills in the task review.

## Execution Loop

For the selected item:

1. Mark the item `In Progress` in `production/backlog.md`, `production/epics/EPIC-###.md` when present, and `production/status.md`.
2. Lock scope from the matching backlog row and task section: task text, acceptance criteria, validation requirements, dependencies, source references, constraints, non-goals, and test plan. The backlog row is an index; the task section is the task contract.
3. For Godot tasks, consult the smallest relevant source reference set selected in preflight.
4. For baseline/scaffold tasks, verify repository hygiene first: `.git/` exists, `.gitignore` exists, and generated/cache/source-output folders are ignored where applicable.
5. For behavior-changing work, create a failing test or validation check first when practical. If not practical, write the manual validation reason in the review file.
6. Implement the smallest vertical slice that satisfies the task.
7. Run deterministic gates before review: relevant lint, typecheck, build, test, playmode, smoke validation, and `git status --short` when repository hygiene is part of the task.
8. Review only the task diff against acceptance criteria, source docs, architecture/ADR fit, consulted engine reference rules, and the `Code Review Gate`.
9. Verify Defined -> Connected -> Reachable:
   - Defined: code/data/content exists where expected.
   - Connected: it is imported, called, referenced, or wired by consumers.
   - Reachable: a player action, game state, test, scene, route, or runtime path can trigger it.
10. Fix review blockers, then rerun deterministic gates.
11. Repeat the fix/review loop up to 3 times.
12. Run the task-local clean/sweep pass only on changed files and direct consumers.
13. Re-run final deterministic gates.
14. Write `production/reviews/[ITEM-ID]-review.md`.
15. If the review verdict is `APPROVED`, set the item `Done` in production files as part of the approved commit. The review must record the planned commit message and staged files, but it must not require its own final commit hash.
16. If the project has git, create the task commit after all task sections, status files, epic status if changed, and review evidence are updated. If running in a child worktree, merge its approved branch back into the active request branch. For an approved standalone task, merge the active request branch into `develop`; a story task stays on that branch until `work-review` closes the story.
17. Update the current story and `production/status.md` in the task branch before its approval merge. Keep status compact: next executable item, blockers, and latest evidence pointer only.

## Review Rules

Use the compact review template. The review must be based on:

- task ID and exact acceptance criteria;
- task section path;
- changed files or diff baseline;
- deterministic gate results;
- relevant design/architecture/ADR references;
- consulted engine reference skills, when applicable;
- Defined -> Connected -> Reachable evidence.

Every task review must include the `Code Review Gate` section. Keep it compact, but it must explicitly cover:

- Correctness: the code matches the task, acceptance criteria, edge cases, and validation results.
- Architecture fit: the change follows existing patterns, respects design/architecture/ADR contracts, and introduces no circular dependencies or unjustified coupling.
- Maintainability: names, structure, abstractions, comments, and cleanup are understandable and do not leave dead code or duplicate implementations.
- Security / safety: user/config/save/external data is treated as untrusted where relevant; no secrets, dangerous execution paths, unsafe file writes, or broken persistence are introduced.
- Performance: no unbounded work, unjustified hot-path allocations, avoidable sync loading, heavy per-frame processing, or unnecessary rendering/physics cost is introduced.

Use these finding severities:

- `Critical`: blocks approval; security issue, data loss, broken functionality, corrupted saves, or unrecoverable runtime failure.
- `Important`: blocks approval unless explicitly deferred with a linked follow-up; likely regression, brittle architecture, missing validation, or significant maintainability/performance risk.
- `Suggestion`: non-blocking improvement; create or update backlog follow-up only when useful.
- `Nit`: optional style/readability note; never blocks approval.

Do not mark a task approved from implementer rationale alone. Evidence must show that the task is implemented, wired, reachable, validated, and reviewed through the `Code Review Gate`. A task cannot be `APPROVED` while any `Critical` or unresolved `Important` finding remains.

For Godot tasks, use changed-file-driven audit triggers rather than broad project audits.

## Commit Rules

Commit only after the task verdict is `APPROVED` and final gates pass.

Stage only:

- files changed for the selected task;
- tests/validation assets changed for the selected task;
- `production/backlog.md`;
- `production/status.md`;
- `production/epics/EPIC-###.md`;
- parent story section when status or task breakdown changed;
- `production/reviews/[ITEM-ID]-review.md`;
- optional task-local bug or evidence files.

Do not stage unrelated user changes or broad cleanup. If unrelated changes are present, leave them unstaged and record that in the review file.

Use one commit per approved task. Use this message format:

```text
<type>(<ITEM-ID>): <imperative summary>
```

The commit body should include:

```text
Work Item: WORK-[NNN]
Review: production/reviews/[ITEM-ID]-review.md
Validation: [commands/checks run]
```

Do not amend the commit just to write its hash into the committed review file. Report the final task commit and, when applicable, parent-branch integration commit. If git is unavailable, record `Commit required: NO - no git repository` in the review. If commit or parent-branch integration fails, update the item to `Blocked` with the exact reason before ending.

## Task-Local Clean/Sweep

Run clean/sweep after implementation and review fixes, before final approval. This is not broad repo cleanup.

Scope the sweep to:

- files changed by this task;
- files directly importing, calling, rendering, or consuming changed files;
- tests added or changed by this task;
- old paths explicitly replaced by this task;
- assets/config/scenes touched by this task.

Remove only confirmed task-local residue. Keep unrelated cleanup out of the task. If cleanup finds unrelated debt, add or update a backlog item instead of changing it.

## Stop Conditions

Stop and update status if:

- acceptance criteria are missing or non-executable;
- required source artifacts are missing;
- the task reveals a design change that affects approved systems, architecture, or ADRs;
- deterministic gates fail and cannot be fixed within this task;
- cleanup reveals unrelated debt that would require broad refactoring;
- an S0/S1 bug blocks the parent story outcome;
- the task is larger than one focused vertical slice.

## Stage Exit

If this task is approved and more selected tasks remain:

```text
Recommended next skill: work-execution
```

If this task is approved and all selected tasks for the parent story are done or returned to the backlog:

```text
Recommended next skill: work-review
```

If blocking bug tasks exist:

```text
Recommended next skill: bug-fix-session
```

If blocking bug epics exist without child tasks:

```text
Recommended next skill: story-shaping
```

If the project state is unclear:

```text
Recommended next skill: status-check
```

