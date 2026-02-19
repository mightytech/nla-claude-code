---
name: code-note
description: Record a codebase observation for later attention. Use this within the NLA to add notes to a managed project's code notes log.
disable-model-invocation: true
---

# Code Note (NLA-side)

Record a codebase observation to a managed project's code notes log. Use this when you're in the NLA and want to add a note to a specific project's `reference/code-notes.md`.

## Execute

1. If no project is specified, check `reference/managed-projects.md` and ask which project.
2. Read the target project's `reference/code-notes.md` to see existing notes and format.
3. Add the new entry at the top of the Notes section.
4. Follow the entry format documented in that file.

## Input

If invoked with arguments, `$ARGUMENTS` may contain the project name and/or the observation.

Otherwise, ask which project and what was noticed.

## Key Guardrails

- **Keep it brief.** Code notes are lightweight by design — a sentence or two.
- **Don't file issues.** This isn't an issue tracker. For bugs or feature requests, use the project's actual issue tracker.
