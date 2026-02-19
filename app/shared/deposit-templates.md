# Deposit Templates

Reference templates for files deposited into code projects. These are structural guides — the NLA generates content tailored to each project, not copies of these templates.

---

## CLAUDE.md (Router Pattern)

The deposited CLAUDE.md acts as a router — it establishes identity and loads focused convention docs based on context. This keeps the top-level file short and scannable.

**Structure:**
```markdown
# [Project Name]

[One sentence: what this project is.]

## How to Work Here

[Brief description of the project's coding philosophy — 2-3 sentences max. This sets
the tone for everything Claude does in this project.]

## Conventions

Read `.claude/docs/conventions.md` for language and project conventions. Follow them
unless the developer explicitly overrides.

[If multiple convention docs exist, route by context:]
[- `.claude/docs/conventions.md` — core language and style conventions]
[- `.claude/docs/testing.md` — testing patterns and requirements]
[- `.claude/docs/deployment.md` — deployment and CI/CD conventions]

## Skills

| Skill | Purpose |
|-------|---------|
| `/friction-log` | Log observations about Claude's behavior in this project |
| `/code-note` | Record a codebase observation for later attention |
[| `/check-feedback` | Triage GitHub issues (if penny post deposited) |]
[| `/write-letter` | Send feedback to another project (if penny post deposited) |]

## Key Files

| Path | Purpose |
|------|---------|
| `.claude/docs/` | Convention and pattern documentation |
| `.claude/skills/` | Skills available in this project |
| `reference/friction-log.md` | Observations about Claude's behavior |
| `reference/code-notes.md` | Codebase observations for later attention |

## Remember

The conventions in `.claude/docs/` are your primary guide. When unsure, check them.
When they're wrong or incomplete, the developer can run `/friction-log` to note the
issue and improve them later.
```

**Notes:**
- Keep the router short — under 60 lines. Details live in the docs it routes to.
- The "How to Work Here" section is the project's personality. It's brief but sets the tone.
- Skills table only lists what was actually deposited.
- Route to convention docs by context when there are multiple.

## conventions.md

Deposited at `.claude/docs/conventions.md`. The primary convention doc for the project.

**Structure:**
```markdown
# Conventions

[Language] conventions for [project name].

## Language and Style

[Language-specific conventions: naming, formatting, imports, etc.]
[Each convention includes WHY, not just what.]

## Code Organization

[How the project is structured. Where things go.]

## Error Handling

[How errors are handled in this project.]

## Testing

[Testing conventions — framework, naming, coverage expectations.]
[May be a separate doc if extensive.]

## Dependencies

[How dependencies are managed. When to add new ones.]
```

**Notes:**
- Start with whatever's relevant. Not every section is needed for every project.
- Import from existing CLAUDE.md content when available.
- Explain the reasoning behind each convention.

## Friction Log (Deposited)

Deposited at `reference/friction-log.md` in the code project. Same structure as the NLA framework's friction log but scoped to Claude Code behavior observations.

**Structure:**
```markdown
# Friction Log

Observations about how Claude Code behaves in this project. Things that surprised you,
didn't work as expected, or worked particularly well.

## How to Use This Log

Run `/friction-log` to add entries. Entries are processed when you (or someone with
the NLA) refines this project's configuration.

### Entry Format

#### YYYY-MM-DD: [Brief title]

- **Type:** output | process | convention
- **Severity:** positive | minor | moderate | significant
- **Observation:** What happened
- **Expected:** What should have happened
- **Context:** What you were doing when you noticed

## Entries

[Newest first]

## Patterns to Watch

- Convention gaps — places where Claude guesses because no convention exists
- Style drift — Claude suggesting patterns inconsistent with project conventions
- Over-helping — Claude adding complexity where simplicity was intended
```

## Code Notes (Deposited)

Deposited at `reference/code-notes.md` and the corresponding skill. A lightweight
observation log for things noticed about the codebase during development.

**Structure:**
```markdown
# Code Notes

Things noticed about the codebase that deserve attention later. Not bugs (use the
issue tracker for those) — observations, improvement ideas, technical debt, patterns
worth discussing.

## How to Use

Run `/code-note` to add entries. Review periodically. Some notes become issues,
some become conversations, some just age out.

### Entry Format

#### YYYY-MM-DD: [Brief title]

- **Area:** [file, module, or system area]
- **Observation:** What you noticed
- **Suggestion:** What might improve it (optional)
- **Priority:** low | medium | worth-discussing

## Notes

[Newest first]
```

## Deposited Skills

### friction-log (Standalone)

Deposited at `.claude/skills/friction-log/SKILL.md`. Standalone — does not reference
the NLA or the framework.

```yaml
---
name: friction-log
description: Log an observation about Claude's behavior in this project
disable-model-invocation: true
---

# Friction Log

Record an observation about how Claude Code is behaving in this project.

## What to Log

- Claude did something unexpected (good or bad)
- A convention wasn't followed
- Claude's suggestions didn't match the project's style
- Something worked particularly well

## How to Log

1. Read `reference/friction-log.md` to see existing entries and the format
2. Add a new entry at the top of the Entries section
3. Fill in the fields that are relevant — not all are required
4. Keep observations specific and actionable

## Input

If invoked with arguments, `$ARGUMENTS` is the observation to log.
Otherwise, ask what the developer noticed.
```

### code-note (Standalone)

Deposited at `.claude/skills/code-note/SKILL.md`. Standalone.

```yaml
---
name: code-note
description: Record a codebase observation for later attention
disable-model-invocation: true
---

# Code Note

Record something you noticed about the codebase that deserves attention later.

## What to Note

- Technical debt worth addressing
- Patterns that could be improved
- Architecture observations
- Things worth discussing with the team

This is lighter than filing an issue. Not everything needs a ticket — some
observations just need to be written down.

## How to Note

1. Read `reference/code-notes.md` to see existing notes and the format
2. Add a new entry at the top of the Notes section
3. Keep it brief — a sentence or two is fine

## Input

If invoked with arguments, `$ARGUMENTS` is the observation to record.
Otherwise, ask what the developer noticed.
```
