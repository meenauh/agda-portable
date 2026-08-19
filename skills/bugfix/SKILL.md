---
name: bugfix
description: Execute exactly one AGDA bug task as a focused worker session for bug-fix-session, including reproduction, severity, fix, validation, review evidence, and backlog/status updates.
---

# AGDA: Bugfix

Use this skill only as the worker contract passed from `bug-fix-session` for one concrete bug task.

It updates:

```text
production/backlog.md
production/status.md
production/reviews/[BUG-ID]-review.md
```

Approved bugfix work must end in a git commit when the project has a git repository.

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Git Worktree Rules

For a git project, all bugfix writes happen in the active request worktree created by `requests-intake`; never implement, edit evidence, or commit from the primary `develop` checkout. Record that worktree path and branch in review evidence. When creating a child bug worktree, immediately copy `develop/.env` into it before dependency installation or execution. A coordinator may use it only when it branches from this active request branch and merges back to it—never directly to `develop`.

It may create:

```text
production/bugs/[BUG-ID].md
```

Separate technical severity from planning priority. A bug can be `S2 / P0` when it blocks the next executable work but is not technically severe. Create a separate bug file only for S0/S1 technical severity, unclear reproduction, or bugs that need investigation history.

## Source Rules

Read:

- `production/backlog.md`, limited to the matching bug epic row and directly related dependency rows when possible
- the matching bug task section in `production/epics/EPIC-###.md` when it exists
- `production/status.md`
- active epic/story/task if any
- latest story review notes if relevant
- related design, architecture, and ADRs only when named by the bug epic row, parent story, reproduction path, or changed files

Use templates:

- `plugins/AGDA/docs/templates/bug.md`
- `plugins/AGDA/docs/templates/task-review.md`

## Method

As soon as the selected bug is identified, set the current session title to its exact ID and title when the active host supports it, for example `BUG-065 Feature unlock celebration`. Do this before classification, reproduction, or implementation; otherwise skip this optional presentation action.

1. Confirm the bug exists as either a standalone bug item or a task section assigned to a parent story. If only a bug report exists, use the bug file as the source of truth. If the bug is large enough to need an epic, ensure the epic section exists; otherwise do not force one.
2. Confirm the current checkout is the active request worktree or an allowed child of it, and its branch is not `develop`.
3. Classify technical severity:
   - `S0`: cannot run, data loss, project-breaking
   - `S1`: blocks the core loop, corrupts state, or prevents a main playable path
   - `S2`: important defect with workaround
   - `S3`: minor issue or polish-level defect
4. Classify planning priority separately:
   - `P0`: blocks closure, milestone gate, or next executable work
   - `P1`: should be fixed soon
   - `P2`: normal backlog bug
   - `P3`: minor/deferred
5. Reproduce the bug or define a clear validation guard if reproduction is not possible.
6. Mark the bug task `In Progress`.
7. Find root cause.
8. Implement the smallest fix.
9. Add a regression test or validation check when practical.
10. Run relevant build/test/validation commands.
11. Write compact review evidence in `production/reviews/[BUG-ID]-review.md`.
12. If validation passes, set the bug task `Done` in production files as part of the approved commit. If the project has git, create the bugfix commit after all fix files, status files, and review evidence are updated. If running in a child worktree, merge its approved branch back into the active request branch. Do not merge to `develop` here.
13. Update status and any affected epic, story, or task state in the bug branch before its approval merge. Keep `production/status.md` compact: next executable item, blockers, and latest evidence pointer only.

## Commit Rules

Commit only after validation passes and the bug review verdict is `APPROVED`.

Stage only:

- files changed for the bugfix;
- tests/validation assets changed for the bugfix;
- `production/backlog.md`;
- `production/status.md`;
- matching epic document section when it exists;
- affected epic file, if any;
- `production/reviews/[BUG-ID]-review.md`;
- optional `production/bugs/[BUG-ID].md`.

Keep detailed reproduction, validation, and fix evidence in `production/reviews/[BUG-ID]-review.md` and optional `production/bugs/[BUG-ID].md`. Do not expand `production/status.md` with full evidence logs.

Do not stage unrelated user changes.

Use this commit message format:

```text
fix(<BUG-ID>): <imperative summary>
```

The commit body should include:

```text
Review: production/reviews/[BUG-ID]-review.md
Validation: [commands/checks run]
```

The review or bug file must record planned commit message and staged files before commit. Do not amend the commit just to write its hash into the committed review file. Report the final bugfix commit and, when applicable, parent-branch integration commit. If git is unavailable, record `Commit required: NO - no git repository` in the review. If commit or parent-branch integration fails, update the bug to `Blocked` with the exact reason before ending.

## Stop Conditions

Stop and update status if:

- the bug cannot be reproduced and no validation guard is possible;
- the fix requires a design change to approved docs;
- the fix conflicts with architecture or ADRs;
- the build/test validation cannot pass.

## Stage Exit

If more blocking bug tasks remain:

```text
Recommended next skill: bug-fix-session
```

If an epic, story, or task still needs execution:

```text
Recommended next skill: status-check
```

Otherwise:

```text
Recommended next skill: requests-intake
```

