# Overview

nla-claude-code is a Natural Language Application that brings NLA capabilities into traditional code projects. Its core job is managing how Claude Code behaves in your codebases — CLAUDE.md configuration, coding conventions, and lightweight developer tools. It works by depositing files into code projects, then iterating on them through friction-driven improvement.

---

## What This NLA Does

This NLA operates on code projects from the outside. You run it in its own directory, tell it which codebase to work on, and it reads, generates, and deposits configuration files into that project. The code project doesn't need to know it's managed by an NLA — the deposited files work standalone in any Claude Code session.

The NLA also deposits *capabilities* — skills like `/friction-log` and `/code-note` that give developers lightweight, LLM-native tools inside their codebases. These aren't just config; they're small applications in their own right.

## Tasks

| Task | What It Does | Source |
|------|-------------|--------|
| Setup Project | First-time setup of a code project — scan, import, deposit | `app/setup-project.md` |
| Manage Project | Ongoing refinement — process friction, update conventions, deposit capabilities | `app/manage-project.md` |

Both tasks have skills (`/setup-project`, `/manage-project`). Manage Project is also triggered conversationally — when the developer names a project or describes a Claude Code behavior problem, CLAUDE.md routes to `app/manage-project.md`.

## How It Connects

```
nla-claude-code (this NLA)
    │
    ├── /setup-project ──→ Scans code project, deposits structure
    │
    ├── Ongoing conversation ──→ Refines conventions, processes friction
    │
    └── /maintain ──→ Edits the NLA itself (its own patterns, templates, behavior)

Code project (managed)
    │
    ├── CLAUDE.md (router) ──→ .claude/docs/ (conventions, patterns)
    │
    ├── /friction-log ──→ reference/friction-log.md (Claude behavior observations)
    │
    └── /code-note ──→ reference/code-notes.md (codebase observations)
```

The improvement cycle:
1. Developer codes with Claude in their project (governed by deposited config)
2. Something's off → `/friction-log` captures it
3. Developer opens this NLA → processes friction into convention improvements
4. Updated conventions are deposited → Claude behaves better next time

## Skills

| Skill | Purpose | Type |
|-------|---------|------|
| `/startup` | Load NLA context at session start | Framework (thin wrapper) |
| `/maintain` | Edit this NLA's behavior and patterns | Framework (thin wrapper) |
| `/friction-log` | Log observations about this NLA's behavior | Framework (thin wrapper) |
| `/validate` | Check system consistency and debug | Framework (thin wrapper) |
| `/preferences` | Edit user preferences | Framework (thin wrapper) |
| `/install` | Install extension packages | Framework (thin wrapper) |
| `/update` | Update installed packages | Framework (thin wrapper) |
| `/check-updates` | Scan for available updates without applying them | Framework (thin wrapper) |
| `/think` | Collaborative design exploration before planning | Framework (thin wrapper) |
| `/debrief` | Reflect on completed work while context is fresh | Framework (thin wrapper) |
| `/close` | Wrap up a session — finalize log, check loose ends | Framework (thin wrapper) |
| `/session-checkpoint` | Mid-session save point — preserve state, refresh context | Framework (thin wrapper) |
| `/guide` | Context-aware help — orient to how the NLA works | Framework (thin wrapper) |
| `/export` | Export this NLA as a plugin | Framework (thin wrapper) |
| `/check-feedback` | Discover and triage feedback from intake channels | Penny post (thin wrapper) |
| `/write-letter` | Draft and submit feedback to another project | Penny post (thin wrapper) |
| `/setup-project` | First-time setup of a code project | Domain skill |
| `/manage-project` | Work on a managed project — process friction, update conventions | Domain skill |
| `/code-note` | Add a code note to a managed project | Domain skill |

## The Improvement Pipeline

**NLA friction** (how the NLA itself behaves):
`/friction-log` in this NLA → `reference/friction-log.md` → `/maintain` processes it → improved patterns and templates

**Project friction** (how Claude Code behaves in a code project):
`/friction-log` in code project → project's `reference/friction-log.md` → conversation in this NLA → improved conventions deposited back

**External feedback** (what others notice):
External feedback → `reference/feedback-log.md` → `/maintain` processes it → improved NLA docs and patterns

All three follow the same shape: observe → record → process → improve. Friction logs are the primary engine. The feedback log captures observations from outside the immediate development loop.

**Extension packages** (`/install`, `/update`) add new capabilities to the NLA. Installed packages are tracked in `reference/installed-packages.md`.

## For Humans: Key Workflows

**Set up a new project:**
Run `/setup-project ../path/to/project`. The NLA scans, imports existing config, and deposits the structure.

**Improve Claude's behavior:**
Code in your project. Notice something. Run `/friction-log`. Come back to this NLA. Discuss what you noticed. The NLA updates conventions and deposits them.

**Add conventions:**
Open this NLA. "I want to add testing conventions to my Python project." Conversational — describe what you want, the NLA writes it and deposits it.

**Add a new capability:**
Open this NLA. "I want a code review checklist skill in my project." The NLA designs and deposits the skill.

**Edit the NLA itself:**
Run `/maintain`. Now you're editing the NLA's patterns, templates, and behavior — not a code project's config.

## Where Things Live

This is the project's as-built structure record — what's here, why it's here, and where each piece came from. Consult this when deciding where a new file belongs. When a structural change is needed (new directory, new top-level file, reorganization), follow the discipline in `CLAUDE.md` / `core/nla-foundations.md` ("Structural Change Discipline"): propose, get approval, update this section in the same operation, then act.

### Project Tree

```
nla-claude-code/
├── CLAUDE.md                    # Runtime identity, modes, execution principles
├── README.md                    # Developer-facing introduction
├── .gitignore                   # Excludes config.md, config/, .claude/settings.local.json
├── .gitmodules                  # Submodule pointers (framework, penny-post)
├── config.md                    # Developer preferences (gitignored)
├── config/                      # Sub-config files (gitignored)
├── .claude/skills/              # Skill wrappers Claude Code discovers
├── app/                         # The application (operative content)
│   ├── overview.md              # This file — how the pieces connect
│   ├── startup.md               # App-specific initialization
│   ├── config-spec.md           # What's configurable
│   ├── setup-project.md         # First-time project setup task
│   ├── manage-project.md        # Ongoing project management task
│   └── shared/                  # Context shared across tasks
├── lib/                         # Traditional code helpers (currently sparse)
├── packages/                    # Submodule dependencies
│   ├── nla-framework/           # NLA Framework — core skills, foundations
│   └── nla-penny-post/          # Penny Post — feedback intake + outbound letters
└── reference/                   # Maintenance records (internal-only)
    ├── design-rationale.md
    ├── friction-log.md          # Pending observations
    ├── friction-log-archive.md  # Resolved
    ├── feedback-log.md          # Accepted external feedback, pending impl
    ├── feedback-log-archive.md
    ├── managed-projects.md      # Registry of code projects this NLA manages
    ├── installed-packages.md    # Install/update log
    ├── system-status.md         # Current state snapshot
    └── sessions/                # Maintenance session logs
```

### Top-Level Files

| Path | Purpose | Attribution |
|------|---------|-------------|
| `CLAUDE.md` | Runtime identity. Default mode (managing code projects), maintenance entry (`/maintain`), execution principles. Loaded automatically by Claude Code. | `[framework default]` per `install/CLAUDE-intent.md`. |
| `README.md` | Developer-facing introduction. | `[framework default]` per `install/structure-intent.md`. |
| `.gitignore` | Excludes `config.md`, `config/`, `.claude/settings.local.json`. | `[framework default]`. |
| `.gitmodules` | Submodule pointers for the framework and penny-post. | `[git/repo convention]`, populated by the packages migration (design-rationale "Migrated to packages/ submodules" 2026-06-05). |
| `config.md` | Developer preferences (verbosity, default deposit choices). Gitignored. | `[framework default]` per `install/structure-intent.md`. |

### `app/` — the application (operative content)

Two channels in this project: `app/` is what the LLM reads and executes; `reference/` is the maintenance channel.

| Path | Purpose | Attribution |
|------|---------|-------------|
| `app/overview.md` | How the NLA's pieces connect (this file). | `[framework default]`. |
| `app/startup.md` | App-specific initialization — status checks for managed projects, friction log, feedback log. Read after framework startup. | `[domain decision]` — added in first-maintenance session 2026-02-19 (see `reference/sessions/2026-02-19-first-maintenance.md`). |
| `app/config-spec.md` | What's configurable in this NLA. | `[framework default]`. |
| `app/setup-project.md` | Task doc: first-time setup of a code project (scan, import, deposit). | `[domain decision]` — core task. |
| `app/manage-project.md` | Task doc: ongoing project management — process friction, update conventions. | `[domain decision]` — core task. |
| `app/shared/values.md` | Commitments and non-negotiables. Loaded at startup. | `[framework default]` per `install/structure-intent.md` (values split from voice 2026-02-22, applied here 2026-06-05). |
| `app/shared/voice.md` | Tone, personality, editorial standards. Task-level prerequisite. | `[framework default]`. |
| `app/shared/common-patterns.md` | Recurring patterns the NLA recognizes (Import Before Overwrite, Deposit Minimally, etc.). | `[domain decision]`. |
| `app/shared/deposit-templates.md` | Templates for files deposited into managed projects. | `[domain decision]` — this NLA's depositing pattern is the distinguishing feature. |

### `.claude/skills/` — skill wrappers

Each wrapper is a short SKILL.md with frontmatter and a delegation pointer. Three groups:

- **Framework thin wrappers** (delegate to `packages/nla-framework/core/skills/`): `startup`, `maintain`, `friction-log`, `validate`, `preferences`, `install`, `update`, `check-updates`, `think`, `debrief`, `close`, `session-checkpoint`, `guide`, `export`.
- **Penny post thin wrappers** (delegate to `packages/nla-penny-post/app/`): `check-feedback`, `write-letter`.
- **Domain skills** (full skills, no delegation): `setup-project`, `manage-project`, `code-note`. These exist only here — they're this NLA's purpose.

### `reference/` — maintenance records (internal)

Not read during normal operation. Consumed by `/maintain`.

| Path | Purpose | Attribution |
|------|---------|-------------|
| `reference/design-rationale.md` | *Why* the NLA is built this way. | `[framework default]`. |
| `reference/friction-log.md` + `-archive.md` | NLA behavior observations. | `[framework default]`. |
| `reference/feedback-log.md` + `-archive.md` | External feedback accepted in triage. | `[framework default]`, added with the penny-post install 2026-02-19. |
| `reference/managed-projects.md` | Registry of code projects this NLA manages. | `[domain decision]` — specific to this NLA's depositing role. |
| `reference/installed-packages.md` | What packages are installed, when, what was applied. | `[framework default]`. |
| `reference/system-status.md` | Current-state snapshot (tasks, skills, packages, recent changes). | `[domain decision]`. |
| `reference/sessions/` | Maintenance session logs (one per substantive session). | `[framework default]`. |

### `packages/` — submodule dependencies

Flat (no `--recursive`). Each NLA pulls its own direct dependencies.

| Path | Purpose | Attribution |
|------|---------|-------------|
| `packages/nla-framework/` | NLA Framework. Core skill logic and foundations. Pinned to a tagged release. | `[framework default]` per design rationale "Migrated to packages/ submodules" (2026-06-05). |
| `packages/nla-penny-post/` | Penny Post. Feedback intake and outbound letters. Optional extension. | `[domain decision]` — opt-in extension chosen during first maintenance. |

### `lib/`

Currently empty (a `.gitkeep` placeholder). Reserved for traditional-code helpers when needed.

### Decision Sources (scan view)

| Decision | Attribution |
|----------|-------------|
| External NLA, deposited files | Design rationale: "External NLA, Deposited Files" |
| Router pattern for deposited CLAUDE.md | Design rationale: "Router Pattern for CLAUDE.md" |
| Standalone deposits (no runtime dependency on this NLA) | Design rationale: "Standalone Deposits" |
| Two friction logs (this NLA's, plus per-project) | Design rationale: "Two Friction Logs" |
| Code notes as a deposit | Design rationale: "Code Notes as a Deposit" |
| Import before overwrite | Design rationale: "Import Before Overwrite" |
| Deposit minimally | Design rationale: "Deposit Minimally" |
| Penny post as optional opt-in | Design rationale: "Penny Post as Optional" |
| Submodules at `packages/` (not sibling dirs) | Design rationale: "Migrated to packages/ submodules" (2026-06-05) |
| `app/startup.md` for app-specific initialization | First-maintenance session 2026-02-19 |
| `reference/managed-projects.md` as managed-project registry | `[domain decision]` — specific to this NLA's purpose |

## Document Index

- [overview.md](overview.md) — How the NLA's pieces connect (this file)
- [startup.md](startup.md) — App-specific initialization (status checks at session start)
- [config-spec.md](config-spec.md) — What's configurable
- [setup-project.md](setup-project.md) — First-time project setup
- [manage-project.md](manage-project.md) — Ongoing project management
- [shared/values.md](shared/values.md) — Commitments and non-negotiables
- [shared/voice.md](shared/voice.md) — Tone and editorial standards
- [shared/common-patterns.md](shared/common-patterns.md) — Common patterns
- [shared/deposit-templates.md](shared/deposit-templates.md) — Deposit templates

## Getting Started

1. Start Claude Code in this directory
2. Run `/startup` to load context
3. Run `/setup-project ../path/to/your/code/project` to set up your first project
4. Code in your project with the deposited configuration
5. Use `/friction-log` in your project when you notice something
6. Come back here to process friction and improve conventions
