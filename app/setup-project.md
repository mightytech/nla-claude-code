# Setup Project

Set up a traditional code project to be managed by this NLA. First-time setup only — ongoing management is conversational.

---

## Purpose

Scan a code project, import any existing Claude Code configuration, and deposit the full structure: router CLAUDE.md, convention docs, and NLA-native skills. The project should be immediately usable with Claude Code after setup, and improvable through the NLA going forward.

## Input

A path to a code project (relative or absolute). The developer may also provide:
- Language/framework context ("it's a Python FastAPI project")
- Specific conventions they want ("we use pytest, black, ruff")
- Preferences about what to deposit ("skip penny post", "include code-note")

## Prerequisites

Read before executing:
1. `app/shared/voice-and-values.md` — how we write and what we value
2. `app/shared/common-patterns.md` — especially "Import Before Overwrite" and "Deposit Minimally"
3. `app/shared/deposit-templates.md` — templates for deposited files

## Processing Steps

### 1. Validate the Target

Confirm the path exists and is a code project (not an NLA). Look for indicators: source code files, package.json/Cargo.toml/pyproject.toml/go.mod, a src/ directory, etc.

If the path doesn't exist or looks like an NLA project, flag it and ask.

### 2. Scan Existing Configuration

Read these files if they exist:
- `CLAUDE.md`
- `.claude/` directory (skills, docs, settings)
- `.cursorrules`, `.windsurfrules`, or other AI assistant configs
- `README.md` (for project context)
- Build/config files (for language/framework detection)

Summarize what you found. If there's existing Claude Code configuration, present it to the developer: "I found an existing CLAUDE.md with these conventions: [summary]. I'll incorporate these into the new structure."

### 3. Determine What to Deposit

**Always deposited (core):**
- `CLAUDE.md` — router pattern pointing to `.claude/docs/`
- `.claude/docs/conventions.md` — language and project conventions
- `.claude/skills/friction-log/SKILL.md` — Claude Code behavior observations
- `.claude/skills/code-note/SKILL.md` — codebase observation log

**Ask about (optional):**
- Penny post wrappers — "Want GitHub issue triage from within this project?"
- Additional convention docs — if the project has complex needs (separate testing conventions, deployment rules, etc.)

### 4. Generate Convention Content

Based on the scan results and developer input:
- Detect the language and framework
- Incorporate any existing CLAUDE.md content
- Generate language-appropriate conventions (naming, testing, error handling patterns)
- Keep it minimal — better to add through iteration than guess wrong

If existing CLAUDE.md content exists, integrate it — don't discard it. The developer put it there for a reason.

### 5. Deposit Files

Create the directory structure:
```
project/
├── CLAUDE.md                          # Router
├── .claude/
│   ├── docs/
│   │   └── conventions.md             # Language + project conventions
│   └── skills/
│       ├── friction-log/SKILL.md      # Claude Code behavior observations
│       └── code-note/SKILL.md         # Codebase observation log
```

If penny post was requested, also deposit:
```
│       ├── check-feedback/SKILL.md
│       └── write-letter/SKILL.md
```

### 6. Update the Registry

Add the project to `reference/managed-projects.md` with:
- Project path
- Date of setup
- Language/framework
- What was deposited
- Notes about existing config that was imported

### 7. Report to the Developer

Summarize what was done:
- Files created (list them)
- Existing content that was incorporated
- What the developer should do next: "Start Claude Code in your project and try coding. When you notice something about Claude's behavior, run `/friction-log`. Come back here to process those observations into convention improvements."

## Judgment Calls

- **Existing CLAUDE.md is extensive and well-organized:** Don't restructure aggressively. Maybe just add the skills and a light router layer. Respect the work that's already there.
- **Project uses multiple languages:** Create separate convention sections or docs per language. The router can load the right one based on file context.
- **Developer is vague about conventions:** Deposit minimal conventions based on language defaults. Better to iterate than to guess.
- **Project already has AI assistant config (Cursor rules, etc.):** Import the relevant parts. These often contain valuable project-specific knowledge.

## What NOT to Do

- Don't modify source code files — only create/edit configuration and documentation
- Don't deposit secrets, environment-specific paths, or credentials
- Don't over-generate conventions — start minimal, iterate forward
- Don't skip the scan — always read what's already there before depositing
