---
name: work-execution
description: Execute all ready tasks for one story by spawning bounded task-execution worker subagents, integrating results, enforcing reviews, and stopping when story review is needed.
---

# AGDA: Work Execution

Use this skill when production has one ready story, whether it is standalone or inside an epic document, with ready task sections.

This skill is the story-level task coordinator. It must spawn worker subagents that follow the `task-execution` skill for task implementation and continue autonomously through the active story until all executable tasks are `Done`, returned to the epic, or blocked. Do not stop between tasks for user approval.

The coordinator verifies worker-owned updates to:

```text
production/backlog.md
production/status.md
production/epics/EPIC-###.md
production/reviews/[STORY-ID]-review.md
```

It may also change project code and tests. Approved task work must end in a git commit when the project has a git repository. Prefer one commit per approved task unless integration requires a single coordinated commit for tightly coupled task results.

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Git Worktree Rules

The coordinator runs inside the active request worktree created by `requests-intake`, never in `develop`. When creating a child task worktree, immediately copy `develop/.env` into it before dependency installation or execution; it branches from the active request branch and merges back to it. Keep the active request branch through story review; `work-review` merges it into `develop` only after final approval.

## Source Rules

Read:

- `production/backlog.md`
- `production/status.md`
- the active epic row in `production/backlog.md`, if one exists
- the active epic document at `production/epics/EPIC-###.md`, if one exists
- the active story section and its child task sections inside the epic document
- any existing story review or bug file for the selected story
- read-first contracts in `preproduction/architecture/technical.md` only if they exist or are named by the epic row
- relevant architecture and ADR references only when referenced by the active epic row, epic document, story section, task sections, or required to resolve implementation details
- if the project uses Godot: `plugins/AGDA/docs/reference-skills/reference-godot-production.md`

Do not read the whole `production/plan.md` or every full design/ADR during normal work execution. Use `production/status.md`, the active epic row, the epic document, the story section, and the task sections as the working set. Consult `production/plan.md` or full design/ADR bodies only when the selected story cannot be interpreted from the row-driven working set.

Use the worker skill contract:

- `plugins/AGDA/skills/task-execution/SKILL.md`

## Story Selection

Select one active story only:

1. If `production/status.md` names an active story, use that story.
2. If status names an active task, use its parent story section.
3. Otherwise, select the first story with shaped child tasks that are `Planned`, `Ready`, `In Progress`, or `Review`.
4. If no story has executable tasks, do not invent work. Recommend `requests-intake` if an epic still needs shaping, `task-execution` if only a standalone task remains, otherwise update status with the blocker.

Immediately set the current session title to the selected work item's exact ID and title when the active host supports it, for example `STORY-031 Cookhouse`. Use the task ID and title when executing a standalone task, the story ID and title for story work, or the epic ID and title only when the selected work has no narrower item. Do this before preflight or worker spawning; otherwise skip this optional presentation action.

## Required Preflight

Before spawning workers:

- Confirm the active epic exists in `production/backlog.md`.
- Confirm the active epic document exists in `production/epics/`.
- Confirm the selected story section exists in the epic document.
- Confirm every selected task section is assigned to the active story.
- Confirm every selected task section has executable acceptance criteria: test passes, observable behavior, or state/file condition.
- Confirm validation/evidence requirements in each task section are explicit.
- Confirm task dependencies are `Done`, not required, or form a dependency-safe execution wave.
- Confirm no selected task requires changing approved systems, architecture, or ADRs first.
- Have each worker record the current git state or changed-file baseline in its own task review file.
- Confirm the active request worktree/branch from `production/status.md` before spawning workers.
- If the project uses Godot, identify the one or two relevant GD Agentic Skills source references per selected task from `reference-godot-production.md`. Do not load the whole source library or full micro-skills by default.

If any preflight check fails, do not implement. Record the blocker in the active request worktree; do not merge it into `develop` before final approval.

## Subagent Coordination Rules

Always use worker subagents for task implementation when subagent tooling is available.

- Spawn one worker subagent per executable task in the current dependency wave.
- Pass each worker the full `plugins/AGDA/skills/task-execution/SKILL.md` text or attach that skill as an input item. Do not assume the worker implicitly has AGDA skills loaded.
- Pass each worker only its assigned task ID, task section, parent story section, matching epic row, relevant constraints, required validation, allowed write scope, and relevant design/architecture/source excerpts.
- Tell each worker its active request worktree or child path/branch, that it must never write in `develop`, and that it must report changed files, validation run, review evidence, parent-branch integration, and blockers. Other agents may be editing the codebase; it must not revert unrelated changes.
- Workers must not expand scope beyond their task section. If they discover follow-up work, they should record it as an epic suggestion instead of implementing it.
- Run tasks sequentially whenever their commits share production tracking files; parallel work is allowed only when write scopes, dependencies, and committed files are genuinely disjoint.
- Dependent or overlapping tasks run sequentially by dependency wave.
- The coordinator verifies evidence and parent-branch integrations, resolves only integration blockers, and decides the next dependency wave. It must not manually copy worker diffs into `develop`.
- If worker subagents are not available, stop and report that work execution requires subagent support for this flow. Do not silently fall back to local single-agent execution unless the user explicitly asks for that fallback.

## Execution Loop

For the active story:

1. Have each worker mark its selected task `In Progress` in its own task worktree.
2. For each selected task, lock scope from the matching epic row, story section, and task section: task text, acceptance criteria, validation requirements, dependencies, source references, constraints, non-goals, and test plan.
3. Spawn worker subagents for the current dependency wave.
4. While workers run, the coordinator may do only non-overlapping integration prep, status consistency checks, or review-template setup. Do not duplicate worker implementation.
5. When workers finish, review their branch diffs and verify each approved child branch is merged into the active request branch.
6. For Godot tasks, confirm each worker consulted the smallest relevant source reference set selected in preflight.
7. For baseline/scaffold tasks, verify repository hygiene: `.git/` exists, `.gitignore` exists, and generated/cache/source-output folders are ignored where applicable.
8. For behavior-changing work, verify there is a failing-first test or validation check when practical. If not practical, require the manual validation reason in the review file.
9. Run deterministic gates before approval: relevant lint, typecheck, build, test, playmode, smoke validation, and `git status --short` when repository hygiene is part of the work.
10. Review only task diffs against acceptance criteria, source docs, architecture/ADR fit, consulted engine reference rules, and the `Code Review Gate`.
11. Verify Defined -> Connected -> Reachable for each completed task:
    - Defined: code/data/content exists where expected.
    - Connected: it is imported, called, referenced, or wired by consumers.
    - Reachable: a player action, game state, test, scene, route, or runtime path can trigger it.
12. Send review blockers back to the responsible worker when possible, then rerun deterministic gates.
13. Repeat the fix/review loop up to 3 times per task.
14. Run the task-local clean/sweep pass only on changed files and direct consumers.
15. Re-run final deterministic gates for the integrated story state.
16. Create the story-review draft in the active request worktree; `work-review` keeps that branch unmerged until story closure is approved.
17. If a task review verdict is `APPROVED`, set that task `Done` in production files as part of the approved commit. The review must record the planned commit message and staged files, but it must not require its own final commit hash.
18. If the project has git, require each worker to commit and merge its approved child branch into the active request branch after task sections, status files, epic files, and review evidence are updated. If either step fails, update the affected task to `Blocked` before continuing.
19. Move to the next dependency-safe task wave and repeat until all active story tasks are `Done`, returned to the epic, or blocked.
20. Require the worker branch to update its task/story state and `production/status.md` before its approval merge. Keep status compact: next executable item, blockers, and latest evidence pointer only.

## Review Rules

Use the compact review template. The review must be based on:

- story ID and exact acceptance criteria;
- epic document path;
- changed files or diff baseline;
- deterministic gate results;
- relevant architecture/ADR references;
- consulted engine reference skills, when applicable;
- Defined -> Connected -> Reachable evidence.

The coordinator must perform a clean-context integration review of worker outputs before marking any task `Done`. It should review the worker's diff and review evidence as written, not rely on the worker's implementation rationale.

Every task review must include the `Code Review Gate` section. Keep it compact, but it must explicitly cover correctness, architecture fit, maintainability, security/safety, and performance. A task cannot be `APPROVED` while any `Critical` or unresolved `Important` finding remains.

For Godot tasks, use changed-file-driven audit triggers rather than broad project audits.

## Commit Rules

Commit only after the task verdict is `APPROVED` and final gates pass.

Stage only:

- files changed for the selected task;
- tests/validation assets changed for the selected task;
- `production/backlog.md`;
- `production/status.md`;
- `production/epics/EPIC-###.md`;
- `production/reviews/[STORY-ID]-review.md`;
- optional task-local bug or evidence files.

Keep detailed validation and review evidence in `production/reviews/[STORY-ID]-review.md`. Do not expand `production/status.md` with command transcripts, full acceptance criteria, or full validation tables.

Use one commit per approved task unless multiple worker outputs are inseparable after integration. Use this message format:

```text
<type>(<STORY-ID>): <imperative summary>
```

The commit body should include:

```text
Story: STORY-[NNN]
Review: production/reviews/[STORY-ID]-review.md
Validation: [commands/checks run]
```

Do not amend the commit just to write its hash into the committed review file. Report the final task and integration commit hashes in the assistant response after each merge succeeds. If git is unavailable, record `Commit required: NO - no git repository` in the review. If commit or integration fails, update the item to `Blocked` with the exact reason before ending.

## Stage Exit

If blocking bug tasks exist:

```text
Recommended next skill: bug-fix-session
```

If the current story is ready for human review:

```text
Recommended next skill: work-review
```

If no ready work remains:

```text
Recommended next skill: requests-intake
```

