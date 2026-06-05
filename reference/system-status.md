# System Status

Current state of nla-claude-code.

**Last updated:** 2026-06-05

## Tasks

| Task | Status | Notes |
|------|--------|-------|
| Setup Project | Active | First-time code project setup — scan, import, deposit |
| Manage Project | Active | Ongoing convention refinement and friction processing |

## Skills

| Skill | Status | Notes |
|-------|--------|-------|
| `/startup` | Active | Framework thin wrapper |
| `/maintain` | Active | Framework thin wrapper |
| `/friction-log` | Active | Framework thin wrapper |
| `/validate` | Active | Framework thin wrapper |
| `/preferences` | Active | Framework thin wrapper |
| `/install` | Active | Framework thin wrapper |
| `/update` | Active | Framework thin wrapper |
| `/check-updates` | Active | Framework thin wrapper |
| `/think` | Active | Framework thin wrapper |
| `/debrief` | Active | Framework thin wrapper |
| `/close` | Active | Framework thin wrapper |
| `/session-checkpoint` | Active | Framework thin wrapper |
| `/guide` | Active | Framework thin wrapper |
| `/export` | Active | Framework thin wrapper |
| `/setup-project` | Active | Domain skill — first-time project setup |
| `/manage-project` | Active | Domain skill — ongoing project management |
| `/code-note` | Active | Domain skill — add code note to managed project |
| `/check-feedback` | Active | Penny post — discover and triage feedback |
| `/write-letter` | Active | Penny post — draft and submit feedback |

## Managed Projects

None yet. Run `/setup-project` to add the first one.

## Installed Packages

| Package | Status | Notes |
|---------|--------|-------|
| NLA Framework | Installed | Core skill logic via thin wrappers |
| Penny Post | Installed | Feedback conventions and skills (`/check-feedback`, `/write-letter`) |

## Recent Changes

- 2026-02-19: Initial creation of nla-claude-code
- 2026-02-19: First maintenance session — architecture review, all findings resolved. Added `/manage-project` skill, installed penny post, created `app/startup.md`, expanded overview pipelines, aligned skill tables.
- 2026-06-05: Framework update session. Migrated to `packages/` submodule layout (framework pinned v0.0.12, penny-post v0.0.1). Added seven framework skills as thin wrappers: `/check-updates`, `/think`, `/debrief`, `/close`, `/session-checkpoint`, `/guide`, `/export`.
