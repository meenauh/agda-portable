---
name: status-check
description: Start or resume AGDA by checking the current game project stage and choosing the next preproduction or production skill.
---

# AGDA: Status Check

Use this as the AGDA start/resume entrypoint and before resuming any interrupted preproduction or production flow. Hosts that expose skills can surface this file directly; hosts with command-style entrypoints can route those commands here.

## Source Rules

Use the local reference material as the authority for this stage:

- `plugins/AGDA/docs/reference-skills/reference-readiness/start/REFERENCE_SKILL.md`
- `plugins/AGDA/docs/reference-skills/reference-readiness/project-stage-detect/REFERENCE_SKILL.md`

## Method

Keep this intentionally short. Inspect existing files before asking questions.

Use local project files as the authority. Do not run broad memory searches for ordinary AGDA routing; use memory only when the user explicitly asks for prior session context or the local files cannot explain the current state.

Check:

- `preproduction/design.md`
- `preproduction/systems.md`
- `preproduction/architecture/technical.md`
- `preproduction/architecture/adrs/*.md`
- `preproduction/architecture/reviews.md`
- `preproduction/production-handoff.md`
- source folders such as `src/`, engine folders, or known game project files
- `prototypes/` or playable evidence
- production artifacts such as `production/plan.md`, `production/backlog.md`, `production/status.md`, `production/epics/*.md`, review files, bug files, and `production/releases/v*.md`

## Output

Return a compact routing report:

- Project type: New game / Existing project / Unknown
- Current stage
- Current epic/story/task, and next executable item when production has started
- Existing evidence
- Missing blockers
- Recommended next skill

## Routing

Use preproduction routing only until production artifacts exist. Once `production/plan.md`, `production/backlog.md`, or `production/status.md` exists, switch to `Production Routing` and do not use missing preproduction architecture or ADRs as ordinary production blockers.

- No brief: `game-conception`
- Brief but no systems map: `systems-mapping`
- Systems map but no technical architecture: `technical-architecture`
- Architecture exists but lacks approved architecture review evidence in `preproduction/architecture/reviews.md`: `technical-architecture`
- Reviewed architecture exists but required ADRs are missing: `adr-creation`
- Required ADRs exist but lack ADR review evidence in `preproduction/architecture/reviews.md` or accepted status: `adr-creation`
- Required ADRs exist and gates are ready but no handoff exists: `production-handoff`
- Production handoff exists but no `production/plan.md`, `production/backlog.md`, or `production/status.md`: `production-planning`
- Production artifacts exist: run the production routing rules below and recommend the next production skill directly.

## Production Routing

When `production/plan.md`, `production/backlog.md`, or `production/status.md` exists, do not route to another detection skill. Inspect production state directly:

1. Verify production has started:
   - If no production handoff exists, recommend `production-handoff`.
   - If handoff exists but production plan/backlog/status are missing, recommend `production-planning`.
2. Identify current stage from `production/status.md` or `production/plan.md`.
3. Identify active epic, story, or task:
   - Prefer `production/status.md`.
   - Otherwise choose the latest backlog row or review file without a matching closure review.
4. Inspect blockers on the active epic, current status snapshot, and latest relevant review row before choosing executable work.
5. Inspect the active epic document's design, story, and task dependencies.
6. Cross-check each selected ID against `production/backlog.md` and `production/epics/`.
7. Determine next production action:
   - Active epic explicitly carries an architecture blocker that cannot be resolved by a scoped ADR: `technical-architecture` for that blocker only.
   - Active epic explicitly carries an ADR blocker or the latest design review names a significant hard-to-reverse or cross-system decision: `adr-creation` for a scoped production ADR.
   - Active epic has design notes that have not been reviewed: `system-design-review`.
   - Active epic needs 2+ stories and has no story/task breakdown: `story-shaping`.
   - Active story has child tasks with `Planned`, `Ready`, `In Progress`, or `Review`: `work-execution` for that story.
   - Active standalone story has child tasks with `Planned`, `Ready`, `In Progress`, or `Review`: `work-execution` for that story.
   - Active standalone task is ready to implement: `task-execution`.
   - Epic or story is complete at the story/task level but human feedback has not been requested or closed: `work-review`.
   - Blocking bug item exists, whether standalone or under an epic: `bug-fix-session`.
   - No ready work remains and completed work exists that has not yet been packaged into release notes: `manage-release`.
   - No ready work remains and at least one epic is still open: `system-design` for the next unfinished epic.
   - No ready work remains and all epics in the backlog are closed: recommend `requests-intake` for the next request or `manage-release` if the current epic has already been packaged.
8. Detect drift:
   - item missing from backlog;
   - referenced epic/story/task section missing;
   - backlog status conflicts with status snapshot;
   - review says approved but backlog not marked done;
   - item marked done without review evidence;
   - bug marked done without validation evidence.

Production routing must not send the project through full `technical-architecture` or foundation ADR creation just because those preproduction artifacts are missing or incomplete. That gate belongs to the preproduction route before production artifacts exist. During production, architecture and ADR routing requires an explicit blocker on the current epic/status/review.

If recommending `work-execution`, include:

```text
Next story: [STORY-ID] - [Title]
Next task wave: [TASK-ID], [TASK-ID], ...
Recommended next skill: work-execution
```

If the current epic is ready for human review:

```text
Recommended next skill: work-review
```

If no ready work remains and at least one epic is still open:

```text
Recommended next skill: system-design
```

If no ready work remains and all epics are closed:

```text
Recommended next skill: requests-intake
```

If active work is ready to close into a release:

```text
Recommended next skill: manage-release
```

Approval evidence means a dated review file written by the matching review loop. A status value by itself is not enough to advance stages.

Ask only one question if the route cannot be inferred from files or the user's prompt.

## Stage Exit

Always end the response with the visible skill the user should call next:

```text
Recommended next skill: [skill-name]
```

Use `none - production flow is complete` only when all gates pass and no AGDA preproduction or production skill remains.
