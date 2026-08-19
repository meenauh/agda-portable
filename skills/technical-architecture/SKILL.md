---
name: technical-architecture
description: Create and review the preproduction baseline architecture, or run the architecture/ADR check used by Requests Intake and explicit production blockers.
---

# AGDA: Technical Architecture

## Git Worktree Boundary

For a production request, run only in the active request worktree recorded by `requests-intake` in `production/status.md`. Write no production artifact from the primary `develop` checkout. Preproduction baseline work is outside this production-request boundary.

Use this skill primarily during preproduction after systems mapping and before production handoff.

Production use includes two cases:

- requests-intake check mode for features and improvements, even when no blocker is expected
- explicit production blocker mode when the active epic needs an architecture decision that cannot be handled by a scoped ADR

Do not rerun or rewrite the full baseline architecture for ordinary Requests Intake unless the request changes the architecture surface.

It creates or updates:

```text
preproduction/architecture/technical.md
preproduction/architecture/reviews.md
```

Do not create ADR files in this skill. List ADR candidates and hand them to `adr-creation`.

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Source Rules

Use the local reference material as the authority for this stage:

- `plugins/AGDA/docs/reference-skills/reference-readiness/create-architecture/REFERENCE_SKILL.md`
- `plugins/AGDA/docs/reference-skills/reference-readiness/architecture-review/REFERENCE_SKILL.md`
- `plugins/AGDA/docs/reference-templates/templates/technical-design-document.md`
- `plugins/AGDA/docs/reference-templates/templates/architecture-traceability.md`
- `plugins/AGDA/docs/templates/architecture-review.md`

## Required Inputs

- `preproduction/design.md`
- `preproduction/systems.md`
- for production blockers only: `production/status.md`, the affected epic row/document, and the latest relevant design review or design delta

If `preproduction/systems.md` contains circular dependencies or an invalid design order, stop and route back to `systems-mapping`. Architecture must not build on a cyclic system map.

## Method

Read `preproduction/design.md` and `preproduction/systems.md` first. Open only the architecture, ADR, or system-map details needed to write the baseline.

If this is a production blocker run, read `production/status.md` and the active epic row/document first, then open only the affected architecture or ADR sections. Limit edits to the impacted architecture contracts, decision summary, traceability row, or ADR candidate trigger. Do not recreate the general architecture or revisit unrelated decisions.

If this is a requests-intake check run, read `production/status.md`, the relevant epic row/document, and the design artifacts touched by the request. Confirm whether the current design implies:

- no architecture blocker
- a scoped ADR candidate
- a broader architecture blocker

Record the result compactly, then return control to `requests-intake`, `adr-creation`, or `technical-architecture` as appropriate.

Build the general architecture from the brief and systems map:

- engine/stack recommendation or chosen stack
- layer map
- module ownership
- runtime/data flow
- save/state model
- API and event boundaries
- toolchain and content pipeline assumptions
- performance, platform, and production constraints
- required ADR candidate list

Authoring status for `technical.md` must start as `Draft - Pending architecture review`. Do not mark architecture `APPROVED` during the authoring pass.

For production blocker runs, keep the existing baseline approval status intact and add a dated `Production Architecture Update` section or compact delta row instead of resetting the whole document to draft. The review should cover only the blocker scope and affected contracts.

## Architecture Review Loop

After drafting `technical.md`, run a separate architecture review pass before leaving this skill. If the same assistant authored the architecture, it must switch into review mode, re-read the artifacts from disk, and review what is written rather than relying on memory of intent.

Review:

- Systems map integrity: no circular system dependencies remain, and the reviewed system dependencies follow the systems map's topological design order.
- ADR coverage: every foundational/cross-system decision is listed as an ADR candidate or explicitly deferred with a trigger.
- Consistency: engine/stack, persistence, state ownership, runtime flow, content pipeline, and platform assumptions do not contradict each other.
- Implementability: production can start without guessing module ownership, data flow, or integration boundaries.
- Scope control: architecture does not introduce systems outside the approved brief/system-map baseline unless marked as deferred.
- Production blocker scope: if this is a production run, the change is limited to the explicit blocker and does not silently reopen unrelated baseline decisions.

Write architecture review evidence to `preproduction/architecture/reviews.md`, not date-split standalone files and not the ADR folder. A no-blocker review can be a single compact row: date, artifact, verdict, notes. If the review finds blockers, add a blocker row in the same file, revise `technical.md` directly, and repeat the review pass. If a production-blocking decision cannot be inferred, ask it during the process and update `technical.md` with the resolved decision. Do not leave unresolved decision backlogs in the architecture document.

## Approval Gate

Do not mark `technical.md` as `APPROVED` unless all of these are true:

- The review pass read `preproduction/design.md` and `preproduction/systems.md` from disk.
- The review checked every item listed in `Architecture Review Loop`.
- `preproduction/systems.md` has no circular dependencies and a valid topological design order.
- `preproduction/architecture/reviews.md` contains a dated architecture review entry with `Verdict: APPROVED`.
- `technical.md` links to the architecture review file.
- Required ADR candidates are clearly separated from deferred candidates.
- Any review revisions were written before the final verdict.

Self-consistency notes from the architecture authoring pass do not count as approval evidence.

## ADR Candidate Timing

List ADR candidates during preproduction when the decision is foundational, cross-system, hard to reverse, or required before coding starts. Examples: engine/stack, save architecture, networking model, simulation ownership, content pipeline, persistence, platform constraints.

Defer an ADR candidate to production only when it is local to one later system, low-risk, or cannot be decided until implementation evidence exists. If deferred, list it in `technical.md` with the trigger that will force the ADR.

`adr-creation` creates the actual ADR files after this skill is done.

During production, add an ADR candidate only when the blocker introduces a new significant decision. If the outcome is only a local implementation detail, update the affected architecture note and route back to `requests-intake` or `story-shaping` without ADR creation.

## Output Shape

Keep `preproduction/architecture/technical.md` concise:

- Summary
- Architecture goals
- Chosen stack / engine
- Layers and ownership
- Data and runtime flows
- System integration contracts
- Read-first contracts and decision summary for downstream production stages
- Production constraints
- ADR index: Required before production / Required before system build / Deferred
- Traceability gaps
- Architecture review link: `preproduction/architecture/reviews.md`

## Architecture Review Output

Create or update:

```text
preproduction/architecture/reviews.md
```

Use this compact shape:

```text
# Architecture Reviews

| Date | Artifact | Verdict | Notes |
|---|---|---|---|
| YYYY-MM-DD | `preproduction/architecture/technical.md` | APPROVED / NEEDS REVISION / BLOCKED |  |

## Blockers

| Date | Artifact | Blocking Issue | Required Change | Resolved |
|---|---|---|---|---|
|  |  |  |  | Yes / No |
```

## Done When

For preproduction, `preproduction/architecture/technical.md` gives production a usable reviewed general architecture, summarizes read-first contracts and decisions, names the foundation/core ADR candidates required before production, gives each deferred ADR candidate a clear production trigger, and links to `preproduction/architecture/reviews.md` with `Verdict: APPROVED`.

For production blocker runs, the explicit blocker is resolved or narrowed to a scoped ADR candidate, the affected epic/status records the result, and review evidence is appended to `preproduction/architecture/reviews.md`.

## Stage Exit

When a requests-intake architecture check run finds no blocker, end the response with:

```text
Recommended next skill: requests-intake
```

When the preproduction architecture review is approved, end the response with:

```text
Recommended next skill: adr-creation
```

When a production architecture blocker is resolved and no scoped ADR is needed, end with:

```text
Recommended next skill: story-shaping
```

When a production architecture blocker is narrowed to a scoped ADR candidate, end with:

```text
Recommended next skill: adr-creation
```

If the architecture remains blocked after asking for required decisions, end with:

```text
Recommended next skill: technical-architecture
```

