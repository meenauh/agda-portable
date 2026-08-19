# Work Item [WORK-ID] Review

## Work Item

- ID:
- Title:
- Verdict: `APPROVED`, `CHANGES REQUIRED`, or `BLOCKED`

## Human Feedback Request

Status: `REQUESTED`, `RECEIVED`, or `SKIPPED BY USER`

Ask the user to test or review the work item before final closure. Generate this checklist from the work-item goal, task outcomes, acceptance criteria, review target, and known risks.

For player-facing work, include only checks the human can perform from the player standpoint inside the game. Do not include scripts, tests, linters, terminal commands, file inspection, commit checks, or internal implementation verification here; those belong in build/test evidence. The agent does not launch or test the game in a browser; this checklist is for human feedback.

### Test Checklist

1. 
2. 
3. 

### Feedback Prompt

Reply with observations, bugs, tuning notes, or `no feedback`.

## Completed Task Summary

Summarize task reviews. Do not paste full task reviews here.

| ID | Title | Verdict | Acceptance / Build Evidence |
| --- | --- | --- | --- |
|  |  | APPROVED / CHANGES REQUIRED / BLOCKED |  |

## Unfinished Tasks

| ID | Title | Reason | Backlog Status |
| --- | --- | --- | --- |
|  |  |  |  |

## Build / Test Summary

| Check | Result | Evidence |
| --- | --- | --- |
|  |  |  |

## Feedback

Only fill this after the user provides feedback or explicitly says `no feedback`.

| Observation | Classification | Backlog Action |
| --- | --- | --- |
|  | Bug / Tuning / Polish / Design Change / Deferred Idea / No Action | Work item created/updated, task created under work item, or no action |

## Bugs Found

| ID | Severity | Priority | Summary | Backlog Status |
| --- | --- | --- | --- | --- |
|  | S0 / S1 / S2 / S3 | P0 / P1 / P2 / P3 |  |  |

## Design Change Candidates

Design changes are work items, not production tasks, until the affected systems and architecture docs are updated.

| Candidate | Affected Docs | Decision |
| --- | --- | --- |
|  |  |  |

## Next Work Implications

- 

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

