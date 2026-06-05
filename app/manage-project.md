# Manage Project

Ongoing management of a code project's Claude Code configuration. This is the NLA's primary ongoing activity — conversational, iterative, driven by developer needs and friction log observations.

---

## Purpose

Refine how Claude Code behaves in a managed code project. Process friction log entries, update conventions, add patterns, adjust the CLAUDE.md router, and deposit new capabilities as needed.

## Input

The developer may:
- Name a specific project to work on ("let's work on my Python app")
- Describe a problem ("Claude keeps suggesting classes when I want functions")
- Ask for a specific change ("add testing conventions to the Rust project")
- Request friction log processing ("what's in the friction log for my-app?")

If no project is specified and multiple projects are managed, ask which one. If no projects are managed yet, suggest running `/setup-project` first.

## Prerequisites

Read before executing:
1. `app/shared/voice.md` — how we write (values are loaded at startup)
2. `app/shared/common-patterns.md` — especially "Convention Docs Explain Why"
3. `reference/managed-projects.md` — which projects are managed and their state
4. `app/shared/deposit-templates.md` — if depositing new files or capabilities

Then read the target project's current configuration:
- Its `CLAUDE.md`
- Its `.claude/docs/` contents
- Its friction log (if processing friction)

## Common Workflows

### Processing Friction

1. Read the project's `reference/friction-log.md`
2. Identify entries about Claude Code behavior (vs. general codebase observations)
3. For each relevant entry, determine the fix:
   - Convention update? → Edit `.claude/docs/conventions.md`
   - New pattern needed? → Add to conventions or create a new doc
   - CLAUDE.md routing issue? → Update the router
   - Skill behavior issue? → Update the relevant skill
4. Present proposed changes to the developer before making them
5. Update the friction log entry status after resolution

### Adding Conventions

1. Understand what the developer wants ("we should always run tests before committing")
2. Check existing conventions to avoid duplication
3. Write the convention with *why*, not just *what*
4. Deposit into the appropriate doc (conventions.md or a new focused doc)
5. Update the CLAUDE.md router if a new doc was created

### Restructuring Configuration

1. Read the current CLAUDE.md and all `.claude/docs/` files
2. Identify what's outgrown its current structure (too long, mixed concerns)
3. Propose a new organization — present it before implementing
4. Restructure files, update the router
5. Verify nothing was lost in the move

### Depositing New Capabilities

1. Understand what the developer wants ("I want a code review checklist skill")
2. Design the skill — what it does, what it reads, what it produces
3. Create the skill file in the project's `.claude/skills/`
4. Update the CLAUDE.md skills table
5. Update the managed-projects registry

## Judgment Calls

- **Friction entry is vague:** Ask the developer to elaborate rather than guessing. "Claude is annoying" needs more context.
- **Convention conflicts with existing code style:** Flag it. The existing codebase is the ground truth — conventions should describe what IS, not what someone wishes it were (unless the developer is intentionally changing direction).
- **Multiple small friction entries about the same theme:** Synthesize into a single convention or pattern update rather than addressing each individually.
- **Developer asks for something that would make Claude less helpful:** Push back gently. "That convention would prevent Claude from suggesting refactoring opportunities — is that intentional?"

## What NOT to Do

- Don't modify source code in the managed project — only configuration and documentation
- Don't make changes without presenting them to the developer first
- Don't assume what the developer wants from a friction log entry — ask if unclear
- Don't deposit capabilities the developer didn't request
