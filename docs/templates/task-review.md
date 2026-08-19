# [ITEM-ID] Review

## Item

- ID:
- Title:
- Type:
- Parent Work Item:
- Verdict: `APPROVED`, `CHANGES REQUIRED`, or `BLOCKED`

## Scope

- Intended slice:
- Out of scope:
- Changed files:

## Acceptance / Evidence

| Acceptance | Evidence | Result |
| --- | --- | --- |
|  |  | PASS / CONCERNS / FAIL |

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
|  | PASS / CONCERNS / FAIL |  |

## Review Findings

| Severity | Finding | Action |
| --- | --- | --- |
|  |  |  |

## Code Review Gate

Review mode: `coordinator`, `clean-context self-review`, or `review subagent`

| Axis | Result | Evidence |
| --- | --- | --- |
| Correctness | PASS / CONCERNS / FAIL |  |
| Architecture fit | PASS / CONCERNS / FAIL |  |
| Maintainability | PASS / CONCERNS / FAIL |  |
| Security / safety | PASS / CONCERNS / FAIL |  |
| Performance | PASS / CONCERNS / FAIL |  |

Finding severity:

- `Critical`: blocks approval; security issue, data loss, broken functionality, corrupted saves, or unrecoverable runtime failure.
- `Important`: blocks approval unless explicitly deferred with a linked follow-up; likely regression, brittle architecture, missing validation, or significant maintainability/performance risk.
- `Suggestion`: non-blocking improvement; create or update backlog follow-up only when useful.
- `Nit`: optional style/readability note; never blocks approval.

Approval requires no unresolved `Critical` or `Important` findings.

## Godot Audit Triggers

Only include for Godot projects and only for changed files/direct consumers.

| Trigger | Check / Script | Result | Evidence |
| --- | --- | --- | --- |
| Signals/events changed | typed signals, callable-style connections, signal loops | PASS / CONCERNS / FAIL / N/A |  |
| GDScript logic changed | type safety, node access, static typing, no brittle paths | PASS / CONCERNS / FAIL / N/A |  |
| Scene/resource/save changed | scene integrity, resource lifecycle, save validation, circular deps | PASS / CONCERNS / FAIL / N/A |  |
| Hot path/process/physics changed | main-thread work, per-frame polling, physics/performance risk | PASS / CONCERNS / FAIL / N/A |  |
| Assets/export/platform changed | naming, imports, export readiness, platform constraints | PASS / CONCERNS / FAIL / N/A |  |

## Fix Loop

Only include when fixes were required after review.

| Iteration | Fixed | Re-run Evidence | Result |
| --- | --- | --- | --- |
|  |  |  |  |

## Changed Files / Commit

- Planned commit message:
- Files intentionally staged:
- Unrelated changes left unstaged:

Do not require this committed review file to contain its own commit hash. Report the final commit hash in the assistant response after the commit succeeds.

## Status Update

- Backlog:
- Work item:
- Status:

## Optional Appendices

Add only when relevant:

- Repository hygiene for scaffold/M0/repo setup work.
- Cleanup notes when cleanup changed files or deferred backlog items.
- Engine/source reference notes when external implementation rules were consulted.

