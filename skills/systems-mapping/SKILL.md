---
name: systems-mapping
description: Decompose an approved game brief into explicit and implicit systems, dependencies, priority tiers, and recommended design order.
---

# AGDA: Systems Mapping

Use this skill after `game-conception`. It creates or updates one output file:

```text
preproduction/systems.md
```

## Documentation Style

Before you create or revise a project document, use `$ste-writing` in STE-flavored mode. Use strict mode for procedures, checklists, and error text. Do not change code, identifiers, or command syntax. Run its self-lint before you save the document.

## Source Rules

Use the local reference material as the authority for this stage:

- `plugins/AGDA/docs/reference-skills/reference-readiness/map-systems/REFERENCE_SKILL.md`
- `plugins/AGDA/docs/reference-templates/templates/systems-index.md`

## Required Input

- `preproduction/design.md`

If the design file is missing, stop and ask to run `game-conception` first.

## Method

Follow the reference systems-mapping workflow closely, compressed into one lean document:

1. Read the brief and any existing `preproduction/systems.md`.
2. Extract explicit systems from mechanics, core loops, technical considerations, and MVP.
3. Infer implicit systems from each explicit system.
4. Present the system list by category and ask for combine/split/cut feedback.
5. Map dependencies using input/output, structural, and UI dependency heuristics.
6. Sort into dependency layers: foundation, core, feature, presentation, polish.
7. Detect circular dependencies and eliminate them before approval.
8. Assign priority tiers: MVP, vertical slice, alpha, full vision/later.
9. Produce the recommended design order as a topological order.

## Dependency Rules

The systems map must be acyclic. Do not approve or complete `preproduction/systems.md` while any circular dependency remains.

When a cycle appears, fix it by changing the system granularity or dependency direction:

- Extract a smaller foundation contract/data model that both systems depend on.
- Split UI/presentation from simulation rules.
- Split data definitions from behavior.
- Split player-facing feature systems from shared technical contracts.
- Replace bidirectional dependencies with one upstream owner and downstream consumers.

The design order must be forward-only:

- Every required system may depend only on systems earlier in the design order.
- If a later system needs information from an earlier one, the earlier system must expose an interface, contract, data model, or extension point broad enough to support that downstream use.
- Later system docs should not require editing earlier system docs except for genuinely discovered corrections during review. If this seems likely, split out a missing foundation system before approving the map.
- Do not use "simultaneous design" as a cycle resolution.
- Do not keep a `Circular Dependencies` section with resolved cycles. The approved output must say there are no circular dependencies.

Do not require exact content lists in this stage. Systems mapping should identify reusable systems and dependencies; use broad content categories when needed instead of exact levels, maps, missions, characters, enemies, items, quests, story beats, assets, or counts.

## Output Shape

Use `../../docs/templates/systems.md`. Do not create per-system design docs in this stage.

## Done When

`preproduction/systems.md` contains:

- Explicit systems.
- Implicit systems.
- Dependency map.
- Acyclic dependency check.
- Priority tiers.
- Recommended design order where every dependency appears earlier than its dependents.
- High-risk systems or validation targets.

Before finishing, re-read `preproduction/systems.md` from disk and verify:

- The dependency map has no cycles.
- The design order is topologically valid.
- No row depends on a later system unless the dependency has been replaced by an earlier foundation contract.
- The output contains `No circular dependencies found.`

## Stage Exit

When this stage is complete, end the response with:

```text
Recommended next skill: system-design
```

