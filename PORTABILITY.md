# Portability

AGDA is model-agnostic and harness-agnostic. The core contract is the Markdown under `skills/`, `docs/`, and `commands/`; a host maps its own actions to the capability words used there.

| AGDA need | Host-independent meaning |
| --- | --- |
| Read or write project files | Use the active workspace filesystem capability. |
| Run validation | Use the project’s documented test, build, lint, or engine checks. |
| Git worktree | Create an isolated branch checkout when Git and the project workflow support it. |
| Worker subagent | Delegate one bounded task when the host provides isolated agent sessions. |
| Rename current chat | Optional presentation action; skip when unsupported. |

The workflow never requires a named foundation model. Hosts may use one model, a routed set of models, or human-directed execution.

## Adapter Metadata

Codex-specific discovery metadata is deliberately isolated to `.codex-plugin/` and `skills/*/agents/openai.yaml`. Other harnesses can load the `SKILL.md` files directly and ignore those paths. A future host adapter should add only discovery or capability-mapping metadata; do not fork the core workflow instructions for a model or vendor.

## Capability Fallbacks

- No subagents: execute a single ready task only when the user explicitly permits a sequential fallback. Otherwise report the coordination blocker.
- No Git worktrees: use the project’s equivalent isolated-branch mechanism, or stop before writing if the project requires worktree isolation.
- No conversation-title API: omit the rename step.
- No browser automation: keep human playtesting as human feedback and use technical checks for validation evidence.
