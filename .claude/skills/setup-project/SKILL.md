---
name: setup-project
description: Set up a code project for management by this NLA. First-time setup — scan, import, deposit.
disable-model-invocation: true
---

# Setup Project

You are setting up a traditional code project to be managed by this NLA. Your job is to scan the project, import existing configuration, and deposit the full structure.

## Execute

Read and follow the instructions in **`app/setup-project.md`**. That document is your primary source of truth for this task.

It will direct you to read prerequisite docs (voice/values, common patterns, deposit templates) if you haven't already. Follow that prerequisite chain.

## Input

If invoked with arguments, `$ARGUMENTS` contains the project path and any additional context.

Otherwise, ask which project to set up.

## Key Guardrails

- **The Cardinal Rule:** The developer decides. Present what you'll deposit and get confirmation before creating files.
- **Flag uncertainty:** When unsure about a convention or structure choice, say so.
- **Import before overwrite.** Always read existing configuration before depositing anything.

## What NOT to Do

- Don't modify source code — only create/edit configuration and documentation
- Don't skip the scan — existing config contains valuable project knowledge
- Don't over-generate conventions — start minimal, iterate forward
- Don't deposit without confirmation — present the plan first
