# Godot Production Reference

Source: https://github.com/thedivergentai/gd-agentic-skills

Local vendored copy:

```text
plugins/AGDA/docs/reference-sources/gd-agentic-skills/
```

Use this reference only for Godot projects during production. Do not load or install the full source library. Select the smallest relevant source skill by work/task domain, then apply its implementation patterns, validation advice, and "NEVER" rules to the current AGDA task.

## Routing

| Work / Task Domain | Source Skill To Consult | Use For |
| --- | --- | --- |
| Godot project scaffold, repo hygiene, feature folders | `godot-project-foundations` | `project.godot`, `.gitignore`, `.gdignore`, feature-based folders, naming conventions |
| Broad Godot architecture choice | `godot-master` | Choosing the relevant Godot pattern chain without loading unrelated domains |
| Headless project automation, imports, scene building, CI/export mechanics | `godot-builder` | CLI/build evidence, scene serialization, import validation, export automation |
| Tests or validation | `godot-testing-patterns` | Unit tests, scene tests, signal tests, deterministic edge cases |
| Debugging or profiling | `godot-debugging-profiling` | Runtime diagnostics, warnings/errors, profiler, memory/orphan checks |
| Signals/events/decoupling | `godot-signal-architecture` | Typed signals, signal up/call down, global bus limits, ghost connection checks |
| Data/resources/saveable definitions | `godot-resource-data-patterns` | `Resource`, `RefCounted`, typed arrays, local-to-scene/duplicate rules |
| Save/load/persistence | `godot-save-load-systems` | Save files, `user://`, migrations, persistence groups |
| Scene transitions/spawning/loading | `godot-scene-management` | async loading, scene lifecycle, packed scenes, dynamic spawning |
| Performance or many-entity work | `godot-performance-optimization` | profiling-first optimization, batching, object pooling, draw-call checks |
| Input/control work | `godot-input-handling` | InputMap, `_unhandled_input`, gamepad/touch/rebinding |
| Release/export work | `godot-export-builds` | smoke tests, export presets, release/debug export separation |
| Feature-specific gameplay | Matching micro-skill from source `skills_index.json` | Combat, inventory, economy, UI, genre, platform, loop, animation, physics, etc. |
| Changed-file code review / audit | `godot-auditor` plus the relevant domain micro-skill | Focused never-list checks, deterministic scripts, and audit evidence for touched files only |

To read a source skill, use:

```text
plugins/AGDA/docs/reference-sources/gd-agentic-skills/skills/[source-skill]/SKILL.md
```

Use `skills_index.json` only to find the smallest matching source skill when the table above is not specific enough.

## Work / Task Application Rules

- Use this reference only after the work-item and task scope are locked.
- Read at most `godot-master` plus the one or two most relevant micro-skills.
- Do not expand the task because a source skill mentions extra best practices; add backlog follow-ups instead.
- Record which source skills were consulted in the task review and work review when relevant.
- Treat relevant "NEVER" rules as review criteria when they touch changed files.

## Godot Review Checklist

Apply only to files touched by the task and their direct consumers:

- Feature-based location is used unless the project has an established different structure.
- Files/folders are snake_case; nodes/classes follow the project's Godot naming convention.
- GDScript is typed where practical; high-frequency containers avoid untyped `Array`/`Dictionary`.
- No brittle absolute node paths, avoidable `get_parent()` coupling, or direct UI-to-data mutation.
- Signals are typed and connected with Godot 4 callable style where practical.
- Runtime state does not mutate shared `.tres` resources; duplicate/localize resources when needed.
- No circular preloads, resource references, or signal loops are introduced.
- Main-thread work, synchronous `load()`, and per-frame polling are justified or avoided.
- New code/content is Defined, Connected, Reachable, and covered by deterministic or manual evidence.

## Changed-File Audit Triggers

Use these triggers during `task-execution` and `work-execution` code review. Do not run broad audits across the whole project unless a changed-file check or validation failure points to a likely project-wide issue.

| Trigger | Consult | Audit Focus |
| --- | --- | --- |
| Signals/events changed | `godot-signal-architecture`, `godot-auditor` | Typed signals, callable-style connections, signal-up/call-down, signal-loop risk, ghost connections |
| GDScript logic changed | `godot-gdscript-mastery`, `godot-auditor` | Explicit types where practical, typed containers, clear class/function boundaries, no brittle paths or avoidable `get_parent()` |
| Scene/resource/save changed | `godot-scene-management`, `godot-resource-data-patterns`, `godot-save-load-systems`, `godot-auditor` | Scene integrity, resource lifecycle, local-to-scene/shared-resource mutation, save validation, circular dependencies |
| Hot path/process/physics changed | `godot-performance-optimization`, relevant physics/input/movement skill, `godot-auditor` | Main-thread work, per-frame polling, allocation churn, synchronous loading, physics/rendering costs |
| Assets/export/platform changed | `godot-project-foundations`, `godot-export-builds`, platform skill, `godot-auditor` | Naming/import policy, generated sidecars, export readiness, platform constraints |

Use deterministic auditor scripts only when the trigger touches changed files or direct consumers and the script can run in the project. If the script is not practical, record a manual audit reason in the task review.

## Code Review Gate

For each Godot task, the task review should summarize the code review gate instead of pasting the source skill text:

- Correctness: task acceptance and edge cases are satisfied.
- Architecture fit: GDD/architecture/ADR contracts and Godot project patterns are respected.
- Maintainability: code is readable, scoped, and free of task-local dead paths.
- Security / safety: file, save, config, external, and user-controlled data are validated when relevant.
- Performance: hot paths avoid unbounded work, avoidable allocations, sync loads, and per-frame overhead.

No task can be approved with unresolved `Critical` or `Important` findings. `Suggestion` and `Nit` findings are non-blocking; create backlog follow-ups only when they have clear value.

