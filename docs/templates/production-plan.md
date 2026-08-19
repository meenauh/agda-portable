# Production Plan

## Source Artifacts

- Handoff:
- Systems map:
- Design folder:
- Architecture:
- ADR folder:

## Production Goal

One paragraph describing the production target this plan is meant to reach.

## Milestones

| ID | Milestone | Purpose | Exit Criteria | Depends On |
| --- | --- | --- | --- | --- |
| M0 | Technical Baseline | Establish a running, testable project baseline. | Build/test command works and the first playable shell exists. | None |
| M1 | Core Loop Prototype | Implement the smallest playable version of the core loop. | Player can complete the core loop end to end. | M0 |
| M2 | Vertical Slice | Deliver one production-quality slice of the intended experience. | Playable slice proves the main systems work together. | M1 |
| M3 | Content Expansion | Expand approved MVP content without changing the core scope. | MVP content is playable and stable. | M2 |
| M4 | Polish / Release Candidate | Stabilize, tune, and prepare for release candidate. | No blocking bugs and release checklist passes. | M3 |

## Epics

Use the same global epic sequence as `production/backlog.md`: if no epic exists, start with `EPIC-000`; otherwise use the highest existing `EPIC-###` plus one. Do not fill gaps.

| ID | Epic | Epic Doc | Source Systems / Architecture | Purpose | Exit Criteria | Depends On |
| --- | --- | --- | --- | --- | --- | --- |
| [EPIC-ID] |  |  |  |  |  |

## Build Order

List epics in the recommended implementation order. The order should be dependency-safe and should not require circular redesign.

1. 

## Production Gates

- M0 must include repository hygiene: `.git/` exists, `.gitignore` covers generated/build/cache/source-output artifacts, and `git status --short` is usable.
- No epic enters the backlog unless it exists in `production/backlog.md` and has a matching epic document.
- No epic closes without acceptance evidence, build/test evidence, and review evidence.
- No story or task closes without a review for that story or task.
- No bug closes without reproduction or validation evidence.
- No design change bypasses the systems map and architecture.

## Strategic Risks

Keep only strategic risks here. If a risk has a concrete mitigation work item, move it to `production/backlog.md` and reference the backlog ID instead of duplicating details.

| Risk | Impact | Backlog Item |
| --- | --- | --- |
|  |  |  |

## Recommended Next Skill

`story-shaping`

