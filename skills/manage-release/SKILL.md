---
name: manage-release
description: Compile a player-facing release from completed production work, determine the next semantic version, and write release notes.
---

# AGDA: Manage Release

Use this skill when the user wants to prepare a release after one or more completed production epics, stories, tasks, bugs, or improvements.

It creates or updates:

```text
production/releases/vX.Y.Z.md
production/releases/vX.Y.Z-backlog.md
production/backlog.md
```

It may also create:

```text
production/releases/
```

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Source Rules

Read:

- `production/backlog.md`
- `production/status.md`
- `production/plan.md` if needed to understand intended scope
- `production/reviews/[ITEM-ID]-review.md`
- existing `production/releases/v*.md` files, newest first

Use the local template:

- `plugins/AGDA/docs/templates/release-notes.md`

## Method

1. Find the latest existing release file in `production/releases/v*.md`.
2. If no release file exists yet, treat this as the first release and start from `v0.1.0`.
3. If a release file exists, read it to identify the last released version and the item IDs included in it.
4. Read `production/backlog.md` and the relevant epic/story/task/bug review files to find items completed after that release.
5. Build the change list from completed items not already included in the last release.
6. Classify each change:
   - `NEW` for new systems, mechanics, features, or player-facing content;
   - `IMPROVED` for tuning, polish, usability, or non-breaking enhancements;
   - `FIXED` for bug fixes and corrected regressions.
7. Determine the next version:
   - major bump only when the user explicitly requests it;
   - if any `NEW` items exist, bump the minor version and reset patch to zero;
   - if only `IMPROVED` and/or `FIXED` items exist, bump the patch version;
   - if there are no changes to release, stop and report that nothing needs publishing yet.
8. If any item is ambiguous between `NEW` and `IMPROVED`, ask the user before writing the release.
9. Compile the release notes in player-facing language only. Keep the final output to three sections:
   - `NEW`
   - `IMPROVED`
   - `FIXED`
10. Rename the current `production/backlog.md` to `production/releases/vX.Y.Z-backlog.md` so the released backlog state is archived with the version.
11. Write `production/releases/vX.Y.Z.md` using the release notes template.
12. Create a fresh `production/backlog.md` for the next cycle, using the backlog template and carrying over only the current routing structure plus any still-open work that remains unreleased.
13. Update `production/status.md` only if the release should change the current next action or latest evidence pointer.

## Version Rules

- Major: `X+1.0.0` only on explicit user request.
- First release: `0.1.0` unless the project already has a clearly established semantic version in `production/releases/`.
- Minor: `X.Y+1.0` when at least one new system or mechanic is present.
- Patch: `X.Y.Z+1` when the release contains only fixes and improvements.

## Output Requirements

The release note file must include:

- version
- release date
- based-on version or previous release reference
- scope as the list of included backlog IDs
- `NEW`
- `IMPROVED`
- `FIXED`

Keep the notes player-facing. Do not include internal analysis, commit hashes, review evidence, or process notes in the published release note file.

## Stage Exit

End with:

```text
Recommended next skill: status-check
```

