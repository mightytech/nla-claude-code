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

## Document Hierarchy

```
app/
├── overview.md                    # This file — how the pieces connect
├── startup.md                     # App-specific initialization (status checks)
├── config-spec.md                 # What's configurable in this NLA
├── setup-project.md               # First-time project setup task
├── manage-project.md              # Ongoing project management task
└── shared/
    ├── values.md                  # Commitments, priorities, non-negotiables (loaded at startup)
    ├── voice.md                   # Tone, personality, editorial standards (task-level)
    ├── common-patterns.md         # Recurring patterns the NLA recognizes
    └── deposit-templates.md       # Templates for files deposited into projects
```

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
