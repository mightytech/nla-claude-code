# nla-claude-code

An NLA that manages how Claude Code behaves in your code projects. Built on the [NLA Framework](https://github.com/mightytech/nla-framework).

## What It Does

This NLA brings NLA capabilities into traditional codebases. It crafts CLAUDE.md files, coding conventions, and lightweight developer tools — then deposits them into your projects where they work standalone in any Claude Code session.

**The core idea:** instead of manually writing and maintaining CLAUDE.md, use an NLA to manage it through conversation and friction-driven iteration.

## Prerequisites

- [Claude Code](https://claude.ai/code) installed
- NLA Framework at `../nla-framework/`

## Quick Start

1. Start Claude Code in this directory
2. Run `/startup` to load context
3. Run `/setup-project ../path/to/your/code/project`
4. Follow the conversation — the NLA scans your project, imports existing config, and deposits the structure
5. Code in your project with the new configuration
6. When you notice something about Claude's behavior, run `/friction-log` in your project
7. Come back here to process observations into improvements

## Directory Structure

```
nla-claude-code/
├── app/                              # The application (what the LLM executes)
│   ├── overview.md                   # How the pieces connect
│   ├── startup.md                    # App-specific initialization (status checks)
│   ├── config-spec.md                # What's configurable
│   ├── setup-project.md              # First-time project setup task
│   ├── manage-project.md             # Ongoing project management task
│   └── shared/
│       ├── voice-and-values.md       # Tone and editorial standards
│       ├── common-patterns.md        # Patterns the NLA recognizes
│       └── deposit-templates.md      # Templates for deposited files
├── reference/                        # Maintenance records
│   ├── design-rationale.md           # Why the system is built this way
│   ├── friction-log.md               # NLA behavior observations
│   ├── friction-log-archive.md       # Resolved friction entries
│   ├── feedback-log.md               # External feedback, pending implementation
│   ├── feedback-log-archive.md       # Resolved feedback entries
│   ├── managed-projects.md           # Registry of managed code projects
│   ├── installed-packages.md         # Installed NLA packages
│   ├── system-status.md              # Current NLA state
│   └── sessions/                     # Maintenance session logs
├── config.md                         # User preferences (gitignored)
├── config/                           # Sub-config files (gitignored)
├── lib/                              # Traditional code helpers
├── .claude/skills/                   # Skills (framework wrappers + domain skills)
├── CLAUDE.md                         # Runtime identity
└── .gitignore
```

## Customization

| File | What to Customize |
|------|-------------------|
| `app/shared/voice-and-values.md` | How the NLA communicates and what it values |
| `app/shared/common-patterns.md` | Patterns the NLA recognizes (grows through use) |
| `app/shared/deposit-templates.md` | Templates for files deposited into projects |
| `app/setup-project.md` | What happens during first-time project setup |
| `app/manage-project.md` | How ongoing project management works |

## Configuration

Run `/preferences` to create or edit your personal configuration. Preferences control things like default deposit choices, managed project paths, and verbosity. See `app/config-spec.md` for what's configurable.

## The Improvement Loop

1. **Observe** — Code in your project. Notice how Claude Code behaves.
2. **Record** — Run `/friction-log` in the code project to capture the observation.
3. **Process** — Open this NLA. Discuss the friction. Improve conventions.
4. **Deposit** — Updated conventions go back to the code project.
5. **Repeat** — Better conventions → better behavior → new observations.

## Adding Capabilities

The NLA can deposit more than just CLAUDE.md configuration. Any skill or tool that works with codebase context can be deposited. To add a new depositable capability, run `/maintain` and describe what you want to add.

## Framework Updates

The NLA Framework lives at `../nla-framework/`. Run `git pull` there to get framework updates — thin wrapper skills pick up changes automatically. Run `/update` to check for and apply package updates.
