---
name: work-review
description: "Review a completed AGDA story in two passes: verify task evidence, request human playtest feedback when relevant, then close or route follow-up work."
---

# AGDA: Work Review

Use this skill after all tasks for a story are done, deferred, blocked, or returned to the backlog, or when the user provides playtest notes for a story.

This is a two-pass skill:

1. Technical review pass: verify epic, story, and task evidence, write/update the story review draft, generate a concrete playtest or operator checklist, then stop and ask the user for feedback when player-facing behavior changed.
2. Closure pass: only after user feedback is provided, or the user explicitly says there is no feedback, classify feedback, update backlog/status, and close the story.

It creates or updates:

```text
production/reviews/[WORK-ID]-review.md
production/backlog.md
production/status.md
production/work/[WORK-ID].md
```

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Git Boundary

Work review runs in the active request worktree created by `requests-intake` after `develop/.env` is copied into it; never write or commit in the primary `develop` checkout. It must verify that every completed task or bug review records its integration into the active request branch. Keep that branch through closure, then merge it into `develop` only when the story is approved.

## Source Rules

Read:

- the parent epic row and its child story/task rows in `production/backlog.md`
- the parent epic document in `production/epics/`
- child task documents in `production/tasks/` only when task review evidence is missing or contradictory
- `production/backlog.md`
- `production/status.md`
- matching `production/reviews/*.md`, summarized by item/verdict/acceptance evidence/build evidence/status first
- build/test evidence listed in the epic, story, and reviews
- user-provided playtest notes if available
- if the project uses Godot: `plugins/AGDA/docs/reference-skills/reference-godot-production.md`

Use the template:

- `plugins/AGDA/docs/templates/work-review.md`

## Method

### Pass 1: Technical Review And Feedback Request

1. Check every completed task under the story.
2. Confirm each completed task has a review file with verdict, acceptance evidence, build/test evidence, and status update.
3. Confirm each completed task or bug review records its active request branch or child integration; return work with missing integration evidence to `Blocked`.
4. Summarize task reviews; do not paste them into the story review and do not fully reread every review body unless evidence is missing, contradictory, failed, or ambiguous.
5. For Godot projects, check whether the task review summaries show relevant source references for changed implementation domains. Full-read only the reviews whose evidence is missing or contradictory.
6. Return unfinished tasks to the backlog with a clear status and reason.
7. Summarize the build or operator result from task evidence. Do not launch or play the game in a browser; player-facing game testing is human feedback only.
8. Create or update `production/reviews/[WORK-ID]-review.md` as a draft.
9. Add a `Human Feedback Request` section:
   - for player-facing work, include a concrete in-game playtest checklist derived from the story goal, completed tasks, acceptance criteria, playtest target, and known risks;
   - for technical/operator work, include only operator-facing checks the human can reasonably verify without inspecting implementation details.
10. Keep player checklists strictly in-game and player-facing. They may ask the user to launch/play the build and perform player actions, but must not ask them to run scripts, tests, linters, terminal commands, inspect files, verify commits, or check internal implementation state. Do not perform these checks through a browser yourself.
11. Ask the user for feedback and stop. Do not classify "no feedback" yourself.

The response must include a concise checklist, for example:

```text
Please review [WORK-ID] before I close it.

Test:
1. [specific player/operator action]
2. [specific expected result]
3. [specific visible edge case/risk]

Reply with observations, bugs, tuning notes, or "no feedback".
Recommended next skill: work-review
```

### Pass 2: Feedback Classification And Closure

Continue only when the user provides feedback or explicitly says `no feedback`.

1. Include the user feedback in the story review.
2. If the user explicitly says `no feedback`, record that as an explicit user response, not as an inferred absence of notes.
3. Classify each feedback item:
   - `Bug`
   - `Tuning`
   - `Polish`
   - `Design Change`
   - `Deferred Idea`
   - `No Action`
4. Add follow-up work to `production/backlog.md` without breaking the backlog hierarchy:
   - create or update an epic for bugs, tuning, polish, design changes, or deferred ideas only when the work is broad enough to need product tracking;
   - create tasks only under an existing story when the follow-up is already concrete and bounded, and record it in the epic document;
   - otherwise recommend `story-shaping` for the follow-up epic.
5. Do not route back to `system-design` from this stage. Any design work for the next epic must already be complete before a story reaches review.
5. Allocate any new epic or task IDs globally by using the highest existing number for that type plus one. Do not fill gaps or restart task numbering per epic.
6. Create optional bug files only for serious or complex bugs.
7. Update `production/status.md` with the next recommended action.
8. After the closure verdict is recorded, commit the review/tracking artifacts in the active request worktree and merge its approved branch into `develop`. If the commit or merge fails, leave the worktree intact and record the exact blocker; do not copy changes into `develop`.

Do not close the story in Pass 1 unless the user has already provided feedback in the same request or explicitly said there is no feedback.

## Design Change Rule

If feedback implies a design change to approved systems, architecture, or ADRs, create or update a design-change epic. Do not implement it as normal production work until the affected docs are updated through the design loop.

## Work Verdict

Use one verdict:

- `ACHIEVED`: story goal met and playable/operator increment exists.
- `PARTIAL`: useful work completed but story goal not fully met.
- `FAILED`: story goal not met or required evidence is missing.

## Stage Exit

If blocking bug tasks exist:

```text
Recommended next skill: bug-fix-session
```

If blocking bug epics exist without child tasks:

```text
Recommended next skill: story-shaping
```

If the backlog still has an open epic after review:

```text
Recommended next skill: system-design
```

If the backlog has no open epic and no release packaging remains:

```text
Recommended next skill: requests-intake
```

If waiting for human feedback:

```text
Recommended next skill: work-review
```

