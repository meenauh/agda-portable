---
name: adr-creation
description: Create and review lightweight ADRs for foundational preproduction decisions or scoped production decisions.
---

# AGDA: ADR Creation

## Git Worktree Boundary

For a production ADR, run only in the active request worktree recorded by `requests-intake` in `production/status.md`. Write no production artifact from the primary `develop` checkout. Preproduction ADR work is outside this production-request boundary.

Use this skill after `technical-architecture` creates and approves `preproduction/architecture/technical.md`.

In preproduction, create the required foundation/core ADRs before production handoff. In production, create only scoped ADRs for explicit significant decisions discovered by Requests Intake, design review, or a current epic blocker.

It creates one file per significant decision:

```text
preproduction/architecture/adrs/[NNNN]-[slug].md
preproduction/architecture/reviews.md
```

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Source Rules

Use the local reference material as the project-specific authority:

- `plugins/AGDA/docs/reference-skills/reference-readiness/architecture-decision/REFERENCE_SKILL.md`
- `plugins/AGDA/docs/reference-templates/templates/architecture-decision-record.md`
- `plugins/AGDA/docs/templates/adr-review.md`

Use lightweight ADR best practice:

- one significant decision per file
- status, decision, why, consequences, applies-to
- options considered only when there is a real non-obvious tradeoff
- append-only history: supersede with a new ADR instead of rewriting accepted decisions
- keep records short, factual, and decision-focused

## Required Inputs

- `preproduction/architecture/technical.md`
- `preproduction/design.md`
- `preproduction/systems.md`
- for production ADRs only: `production/status.md`, the affected epic row/document, and the design review or epic blocker that requires the ADR

If `technical.md` is missing or does not link to an approved architecture review entry in `preproduction/architecture/reviews.md`, stop and run `technical-architecture` first.

For production ADRs, do not require a full architecture rerun when the baseline architecture already exists and the blocker is one scoped decision. If the blocker is broader than one decision, route to `technical-architecture` first with the blocker scope.

## What Needs An ADR

Create an ADR when a decision is:

- foundational or hard to reverse
- cross-system
- tied to performance, persistence, networking, save/state, engine/stack, content pipeline, platform constraints, or tooling
- required before production coding starts
- likely to be debated or forgotten without a record
- explicitly marked as an architecture/ADR blocker on a production epic, status snapshot, or design review

Do not create an ADR for:

- minor implementation details
- obvious local choices inside one low-risk system
- temporary prototype code
- decisions already fully captured by an accepted ADR

## Method

1. Read `technical.md` and find the ADR candidate list.
2. Split compound candidates into one decision per ADR.
3. Number the next ADR sequentially from existing files.
4. Draft only the ADRs marked required before production or required before the next system build.
5. Leave deferred decisions in `technical.md` with a clear trigger instead of creating premature ADRs.

For production ADRs:

1. Read `production/status.md` and the affected epic row/document first.
2. Read the latest design review or blocker note that triggered the ADR.
3. Read only the affected architecture, system, or ADR sections.
4. Draft one ADR for the scoped decision.
5. Update `technical.md` ADR index or production-decision summary with the accepted ADR reference.
6. Update the affected epic/status blocker so story shaping can resume.

Authoring status for new ADRs must be `Proposed`. Do not mark an ADR `Accepted` during the authoring pass.

## ADR Review Loop

After drafting all required ADRs, run a separate ADR review pass across the ADR set before leaving this skill. If the same assistant authored the ADRs, it must switch into review mode, re-read `technical.md`, the relevant systems map, and every required ADR from disk, and review what is written rather than relying on memory of intent.

Read `preproduction/architecture/technical.md` and its ADR index first. Open only the architecture, systems, or ADR sections needed for the decision under review.

Write ADR review evidence to `preproduction/architecture/reviews.md`, not to `preproduction/architecture/adrs/`. The ADR folder is only for decision records. A no-blocker review can be a single compact row: date, artifact, verdict, notes. Add blocker rows only when a review is not approved.

Review:

- Coverage: every required ADR candidate in `technical.md` has either an ADR file or an explicit deferral.
- Atomicity: each ADR contains one significant decision, not a bundle of unrelated decisions.
- Context: each ADR links to the architecture and relevant system requirements.
- Options: `Options Considered` exists only when the decision is non-obvious and had a real tradeoff. Do not expand obvious choices with artificial alternatives.
- Decision quality: the chosen option follows from the context and tradeoffs.
- Consequences: positive, negative/tradeoff, and follow-up consequences are recorded.
- Consistency: ADRs do not contradict each other or `technical.md`.
- Production scope: if this is a production ADR, it resolves only the explicit epic/design-review blocker and does not invent unrelated architecture work.

If review finds issues, revise the affected ADRs and rerun the ADR review pass. If a required decision cannot be inferred, ask it during the process and update the affected ADRs before continuing. Do not leave unresolved decision backlogs in ADR files.

## Acceptance Gate

Do not mark an ADR as `Accepted` unless all of these are true:

- The ADR review pass read `technical.md`, relevant system references, and all required ADRs from disk.
- The ADR review checked every item listed in `ADR Review Loop`.
- `preproduction/architecture/reviews.md` contains a dated ADR review entry with `Verdict: APPROVED`.
- Each accepted ADR links to the ADR review file.
- Any review revisions were written before the status changed to `Accepted`.
- `technical.md` ADR index is updated to show the ADR as accepted.

Self-consistency notes from the ADR authoring pass do not count as acceptance evidence.

## Output Shape

Use this compact template:

```text
# ADR-[NNNN]: [Decision Title]

Status: Proposed / Accepted / Superseded

## Decision

The chosen decision in one or two sentences.

## Why

Problem, constraints, relevant system requirements, and why this matters now.

## Consequences

- Positive:
- Tradeoff:
- Follow-up:

## Applies To

- Architecture: `preproduction/architecture/technical.md`
- Systems / requirements:
- Review: `preproduction/architecture/reviews.md`
- Supersedes / Superseded by:

## Options Considered

Only include this section for non-obvious decisions with a real tradeoff.

- Option A:
- Option B:
```

## ADR Review Output

Create or update:

```text
preproduction/architecture/reviews.md
```

Use this compact shape:

```text
# ADR Reviews

| Date | Artifact | Verdict | Notes |
|---|---|---|---|
| YYYY-MM-DD | `preproduction/architecture/adrs/[NNNN]-[slug].md` | APPROVED / NEEDS REVISION / BLOCKED |  |

## Coverage

| Candidate | ADR / Deferral | Status |
|---|---|---|
|  |  |  |

## Blockers

| Date | Artifact | Blocking Issue | Required Change | Resolved |
|---|---|---|---|---|
|  |  |  |  | Yes / No |
```

## Done When

For preproduction, all foundation/core ADRs required before production have `Status: Accepted` and link to `preproduction/architecture/reviews.md` with `Verdict: APPROVED`, or `technical.md` explicitly lists why a decision is deferred and what will trigger it.

For production, the scoped ADR has `Status: Accepted`, the affected epic/status no longer carries the ADR blocker, and the next work can resume at story shaping.

## Stage Exit

When required preproduction ADRs are accepted or explicitly deferred, end the response with:

```text
Recommended next skill: production-handoff
```

When a scoped production ADR is accepted, end the response with:

```text
Recommended next skill: story-shaping
```

If ADR creation remains blocked after asking for required decisions, end with:

```text
Recommended next skill: adr-creation
```

