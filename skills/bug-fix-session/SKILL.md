---
name: bug-fix-session
description: Orchestrate AGDA bug fixes by spawning one bugfix worker subagent per bug item, integrating results, and stopping for review or blockers.
---

# AGDA: Bug Fix Session

Use this skill when one or more concrete bug items are ready to fix in production. Bug items may live by themselves or under a bug epic.

This is the bug-level coordinator. It must spawn a separate worker subagent for each executable bug item and pass the `bugfix` worker contract to each worker. Do not combine multiple bugs into one worker session.

The coordinator verifies worker-owned updates to:

```text
production/backlog.md
production/status.md
production/epics/EPIC-###.md
production/reviews/[BUG-ID]-review.md
production/bugs/[BUG-ID].md
```

Approved bug work must end in a git commit when the project has a git repository.

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Git Worktree Rules

The coordinator runs inside the active request worktree created by `requests-intake`, never in `develop`. When creating a child bug worktree, immediately copy `develop/.env` into it before dependency installation or execution; it branches from the active request branch and merges back to it. When the complete bug session is approved, merge the active request branch into `develop`; retain it on conflict and do not copy changes into `develop`.

## Source Rules

Read:

- `production/backlog.md`
- `production/status.md`
- the matching epic row for each selected bug, if one exists
- the matching bug section in `production/epics/EPIC-###.md`, if one exists
- any existing bug file or review file for the selected bug
- related design or engine references only when named by the bug, the epic, or the changed files
- if the project uses Godot: `plugins/AGDA/docs/reference-skills/reference-godot-production.md`

Use the worker skill contract:

- `plugins/AGDA/skills/bugfix/SKILL.md`

## Bug Selection

Select one or more executable bugs:

1. If `production/status.md` names an active bug, resume that bug.
2. Otherwise, select the first bug item with status `Planned`, `Ready`, `In Progress`, or `Review`.
3. Only group bugs together when their write scopes do not conflict or when they clearly need shared decomposition. Because every bug branch updates shared production tracking files, run bugs sequentially unless their commits genuinely have no shared-file overlap.
4. If no bug item is executable, do not invent work. Recommend `work-execution` if story work remains, otherwise `requests-intake`.

## Required Preflight

Before spawning workers:

- Confirm each selected bug exists in `production/backlog.md`.
- Confirm each selected bug has either a matching bug file or a matching section in `production/epics/EPIC-###.md`.
- Confirm each selected bug has executable acceptance criteria.
- Confirm each selected bug has explicit validation or evidence requirements.
- Confirm dependencies are `Done`, not required, or already cleared.
- Confirm the bug does not require a design change to approved systems, architecture, or ADRs first.
- Have each worker record the current git state or changed-file baseline in its own bug review file.
- Confirm the active request worktree/branch from `production/status.md` before spawning workers.
- If the project uses Godot, identify the one or two relevant GD Agentic Skills source references per selected bug from `reference-godot-production.md`.

If any preflight check fails, do not implement. Record the blocker in the active request worktree; do not merge it into `develop` before the bug session is approved.

## Subagent Coordination Rules

Always use worker subagents for bug implementation when subagent tooling is available.

- Spawn one worker subagent per executable bug item in the current dependency wave.
- Pass each worker the full `plugins/AGDA/skills/bugfix/SKILL.md` text or attach that skill as an input item.
- Pass each worker only its assigned bug ID, bug section, parent epic row, relevant constraints, required validation, allowed write scope, and relevant design or engine excerpts.
- Tell each worker its active request worktree or child path/branch, that it must never write in `develop`, and that it must report changed files, validation run, review evidence, parent-branch integration, and blockers. Other agents may be editing the codebase; it must not revert unrelated changes.
- Workers must not expand scope beyond their bug section.
- The coordinator verifies evidence and parent-branch integrations, resolves only integration blockers, and decides the next dependency wave. It must not manually copy worker diffs into `develop`.
- If worker subagents are not available, stop and report that bug-fix session requires subagent support for this flow.

## Execution Loop

For the selected bugs:

1. Have each worker mark its selected bug `In Progress` in its own bug worktree.
2. Lock scope from the matching backlog row and bug section: bug text, acceptance criteria, validation requirements, dependencies, source references, constraints, non-goals, and test plan.
3. Spawn worker subagents for the current dependency wave.
4. While workers run, do only non-overlapping integration prep, status consistency checks, or review-template setup.
5. When workers finish, review their branch diffs and verify each approved child branch is merged into the active request branch.
6. For Godot bugs, confirm each worker consulted the smallest relevant source reference set selected in preflight.
7. Run deterministic gates before approval: relevant lint, typecheck, build, test, smoke validation, and `git status --short` when repository hygiene is part of the work.
8. Review only bug diffs against acceptance criteria, source docs, architecture or ADR fit, consulted engine reference rules, and the `Code Review Gate`.
9. Verify Defined -> Connected -> Reachable for each completed bug.
10. Send review blockers back to the responsible worker when possible, then rerun deterministic gates.
11. Repeat the fix/review loop up to 3 times per bug.
12. Run the bug-local clean/sweep pass only on changed files and direct consumers.
13. Re-run final deterministic gates for the integrated bug state.
14. Require each worker to write `production/reviews/[BUG-ID]-review.md` in its own bug worktree.
15. If a review verdict is `APPROVED`, set the bug `Done` in production files as part of the approved commit.
16. If the project has git, require each worker to commit and merge its approved child branch into the active request branch after bug sections, status files, epic files, and review evidence are updated. When all selected bugs are approved, merge the active request branch into `develop`. If either step fails, update the affected bug to `Blocked` before continuing.
17. Move to the next dependency-safe bug wave and repeat until all active bug items are `Done`, returned to the epic, or blocked.
18. Require the worker branch to update its bug and `production/status.md` before its approval merge. Keep status compact: next executable item, blockers, and latest evidence pointer only.

## Stage Exit

If more blocking bug items remain:

```text
Recommended next skill: bug-fix-session
```

If story work still needs execution:

```text
Recommended next skill: work-execution
```

Otherwise:

```text
Recommended next skill: requests-intake
```

