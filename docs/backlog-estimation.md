# Backlog Estimation

## Recommendation

Use one additive `volume` budget per release, capped at `100`.

- `epics` are containers and do not count directly.
- `stories` count only when they are standalone work.
- `tasks` and `bugs` are the normal counting unit.
- Every counted item gets one volume number.
- The release total is the sum of the leaf items only.

This gives one clean number for both planning and progress:

- `scope loaded = planned leaf volume / 100`
- `completeness = done leaf volume / 100`

## Point Scale

Use a small fixed scale. Do not estimate in hours.

| Volume | Meaning |
| --- | --- |
| 1 | Tiny, obvious, same-file or single-step work |
| 2 | Small, low-risk, limited surface area |
| 3 | Modest, a few touches, little uncertainty |
| 5 | Medium, crosses files or one dependency |
| 8 | Large, cross-system, or integration-heavy |
| 13 | Split first unless there is no clean split |

Anything larger than `13` is not a planning unit. Split it.

## Rollup Rule

Never count the same work twice.

- Epic volume = sum of child story or task leaf volume.
- Story volume = sum of child task or bug volume, or direct estimate if the story is standalone.
- Task or bug volume = direct estimate.

If an epic has 3 stories and each story has tasks, only the tasks count toward release volume unless a story is intentionally standalone.

## Release Rules

- `planned leaf volume >= 100` means the backlog for that release is full.
- `done leaf volume >= 100` means the release target is met, assuming quality gates also pass.
- `planned leaf volume >= 90` should warn that new scope needs to replace old scope.
- `planned leaf volume >= 100` should stop new intake for that version.
- Trigger the "backlog full" alert at `planned leaf volume >= 100`.

This is a scope budget, not a ship-it-by-number override. A release still needs passing validation and no blocking bugs.

## Example

- Epic A contains two stories worth 21 total.
- Epic B contains one standalone story worth 8 and two bugs worth 3 each.
- Epic C contains tasks worth 42.

Total planned volume = `21 + 8 + 3 + 3 + 42 = 77`.

If `29` of that is done, status reads:

- `completeness: 29/100`
- `scope loaded: 77/100`

If the team adds another `24` points of scope, planned volume becomes `101` and the release is full.

## Why This One

I did not pick the other common options because they fail one of the two things you actually need: a clean release cap and a truthful progress number.

- `Hours` are too tied to person speed and calendar noise.
- `T-shirt sizes` are too coarse to sum into a useful release budget.
- `Story points without rollup rules` double count or hide the real total.
- `Item counting` treats a tiny bug and a major integration as the same thing.
- `Percent complete per item` does not roll up cleanly across a backlog hierarchy.

This model is the smallest one that still gives:

- one release budget,
- one progress number,
- one alert at full scope,
- and no double counting.

## How To Use It In AGDA

AGDA should keep `production/backlog.md` epic-only.

Store the point values in the epic docs where the stories, tasks, and bugs live. Then summarize only the active release budget in `production/status.md`.

Recommended status line:

- `completeness: 52/100`
- `scope loaded: 74/100`

That is enough to decide whether to keep taking work or freeze scope for release.
