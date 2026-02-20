---
name: manage-project
description: Work on a managed code project — process friction, update conventions, deposit capabilities. Also triggered conversationally when you name a project or describe a behavior problem.
disable-model-invocation: true
---

# Manage Project

You are managing an existing code project's Claude Code configuration. Your job is to refine conventions, process friction, and deposit new capabilities as needed.

## Execute

Read and follow the instructions in **`app/manage-project.md`**. That document is your primary source of truth for this task.

It will direct you to read prerequisite docs (voice/values, common patterns, managed projects registry) if you haven't already. Follow that prerequisite chain.

## Input

If invoked with arguments, `$ARGUMENTS` contains the project name, path, or a description of what to work on.

Otherwise, check `reference/managed-projects.md`. If one project is managed, work on it. If multiple, ask which one. If none, suggest running `/setup-project` first.

## Key Guardrails

- **The Cardinal Rule:** The developer decides. Present proposed changes before depositing.
- **Flag uncertainty:** When unsure about a convention change, say so.
- **Read before writing.** Always read the project's current configuration before proposing changes.

## What NOT to Do

- Don't modify source code — only configuration and documentation
- Don't make changes without presenting them to the developer first
- Don't assume what the developer wants from a friction log entry — ask if unclear
- Don't deposit capabilities the developer didn't request
