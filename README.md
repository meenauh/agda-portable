# AGDA

AGDA (Agentic Game Dev Assistant) is a portable, model-agnostic workflow for taking a game from conception through release. Its core is a collection of plain Markdown skills and templates; it does not require a particular model, agent framework, provider, or tool protocol.

## What Is Portable

- `skills/` contains the workflow instructions in a common, Markdown-first format.
- `docs/` contains framework-neutral references and templates.
- The workflow asks a host to use capabilities such as filesystem access, Git, tests, and optional subagents, but does not require a specific implementation of them.
- If a host cannot rename a conversation or launch subagents, it should skip the cosmetic title action and either execute sequentially when authorised or report the missing capability where parallel coordination is required.

The optional `.codex-plugin/` manifest and `agents/openai.yaml` files are adapter metadata for Codex discovery only. They do not define the workflow and can be ignored by other harnesses.

See [PORTABILITY.md](PORTABILITY.md) for integration guidance.

## Start Here

Load `skills/status-check/SKILL.md` to start or resume a project. Load `skills/requests-intake/SKILL.md` when a new feature, improvement, or bug request arrives. Each skill names its inputs, outputs, checks, and next routing step.

## Workflow

Preproduction:

1. Status check
2. Game conception
3. Systems mapping
4. Technical architecture and ADRs
5. Production handoff

Production:

1. Production planning
2. System design and review, when the epic needs refinement
3. Architecture check and a scoped ADR when needed
4. Story shaping
5. Work execution and task execution
6. Work review with human player feedback when relevant
7. Release management

`production/status.md` is the active routing snapshot. `production/backlog.md` routes production work, while detailed epic, story, task, and review information remains in its dedicated document.

## Contents

- `skills/` — active workflow stages.
- `docs/templates/` — project artifact templates.
- `docs/reference-sources/` — retained, licensed implementation references.
- `.codex-plugin/` and `skills/*/agents/openai.yaml` — optional Codex adapter metadata.

## Licenses And Sources

AGDA is available under the MIT License. Bundled third-party source material remains under its included license files: `LICENSE-AGDA-BRIEF`, `LICENSE-AGDA-READINESS`, and `LICENSE-AGDA-GODOT-REFERENCE`.
