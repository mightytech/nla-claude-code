# Architecture Review: nla-claude-code

**Date:** 2026-02-19

## Document Chain

```
CLAUDE.md (always loaded)
├── Directs: run /startup at session start
├── References: app/overview.md, app/manage-project.md, app/config-spec.md
├── References: reference/managed-projects.md
└── Routes to skills based on user input

/startup → .claude/skills/startup/SKILL.md → ../nla-framework/core/skills/startup.md
├── 1. ../nla-framework/core/nla-foundations.md
├── 2. app/overview.md
├── 3. app/shared/voice-and-values.md
├── 4. app/shared/common-patterns.md
├── 5. app/shared/output-spec.md (conditional — does not exist)
├── 6. config.md (conditional — exists)
│   └── config/maintenance.md (loaded in maintenance context)
└── 7. app/startup.md (conditional — does not exist)

/setup-project → .claude/skills/setup-project/SKILL.md → app/setup-project.md
├── prereq: app/shared/voice-and-values.md
├── prereq: app/shared/common-patterns.md
├── prereq: app/shared/deposit-templates.md
└── updates: reference/managed-projects.md

Manage Project (no skill — conversational routing from CLAUDE.md) → app/manage-project.md
├── prereq: app/shared/voice-and-values.md
├── prereq: app/shared/common-patterns.md
└── prereq: reference/managed-projects.md

/maintain → .claude/skills/maintain/SKILL.md → ../nla-framework/core/skills/maintain.md
├── prereq: reference/design-rationale.md
├── prereq: ../nla-framework/core/nla-foundations.md
├── prereq: app/overview.md
├── prereq: reference/friction-log.md
└── prereq: reference/feedback-log.md
```

## Findings

### Fix

(none)

### Improve

1. **`app/overview.md`**: Improvement pipeline section only shows friction-driven improvement. The feedback pipeline (external feedback → feedback-log → `/maintain`) is not represented, even though the feedback log exists and `/maintain` explicitly processes it. A reader of the overview would not know the feedback pipeline exists. — **Conditional completeness**

2. **`app/manage-project.md`**: Prerequisites list voice-and-values, common-patterns, and managed-projects — but the "Depositing New Capabilities" workflow requires knowledge of deposit templates (`app/shared/deposit-templates.md`). Missing prerequisite could cause the LLM to improvise skill file structure instead of following the templates. — **Prerequisite sufficiency**

3. **`app/manage-project.md`**: Handles "no project specified + multiple projects" (ask which one) but doesn't handle "no managed projects at all." If a developer enters a management conversation before any projects are set up, the doc doesn't guide the LLM to suggest `/setup-project`. CLAUDE.md's routing handles this for named paths ("if new, suggest /setup-project"), but manage-project.md itself has the gap. — **Conditional completeness**

4. **Multiple files**: Penny post is referenced in `setup-project.md` (offered during setup), `deposit-templates.md` (router entries for `/check-feedback` and `/write-letter`), `config-spec.md` (deposit option), and `design-rationale.md` (design decision). But there's no clear mechanism to actually obtain the skill content. If it's an installable package, that's not stated anywhere. If the NLA is supposed to generate the skills itself, there are no templates for the skill file content (only the CLAUDE.md router entries). The path from "developer says yes to penny post" to "working skills deposited" has a gap. — **Cross-reference integrity / Conditional completeness**

5. **`CLAUDE.md` vs `app/overview.md`**: Skill purpose descriptions differ slightly between the two tables. Examples: "Log observations about this NLA" vs "Log observations about this NLA's behavior"; "Check system consistency" vs "Check system consistency and debug"; "Add a code note to a managed project" vs "Add a code note to a managed project (from NLA side)". Not wrong, but creates minor drift that could compound over time. — **Consistency**

### Note

1. **`app/overview.md`**: Manage Project is the only task without a corresponding skill. It's triggered conversationally via CLAUDE.md routing, which works, but this asymmetry isn't documented. The tasks table lists two tasks; the skills table lists nine skills; the relationship between them isn't explicit. Future maintainers might wonder why there's no `/manage-project` skill. — **Layer boundaries**

2. **`app/startup.md` does not exist**: The framework startup skill checks for app-specific initialization at `app/startup.md`. This NLA doesn't have one yet. Not a problem now, but it's the natural hook for features like "check for active work in managed projects" or "show managed project status at session start." Worth knowing as a growth point. — **Conditional completeness**

3. **`reference/installed-packages.md`**: Listed in README.md directory tree but not referenced in `app/overview.md` or `CLAUDE.md`. Presumably managed by `/install` and `/update`, but invisible to the documented architecture. Minor orphan risk. — **Orphaned content**

## Summary

8 findings: 0 fix, 5 improve, 3 note. All resolved during the 2026-02-19 maintenance session.

## Resolutions

All findings were addressed in the maintenance session that followed this review:

1. **Overview pipeline** — Expanded to three pipelines (NLA friction, project friction, external feedback) plus extension packages. → `app/overview.md`
2. **manage-project prerequisites** — Added `deposit-templates.md` as conditional prerequisite. → `app/manage-project.md`
3. **Zero-projects case** — Added guidance to suggest `/setup-project`. → `app/manage-project.md`
4. **Penny post mechanism** — Installed penny post via `/install`. Made setup-project offer conditional on availability. Added deposit templates for thin wrapper skills. Documented opt-in dependency decision. → multiple files
5. **Skill description drift** — Normalized all five drifted descriptions across CLAUDE.md and overview.md. → `CLAUDE.md`, `app/overview.md`
6. **Manage Project skill** — Created `/manage-project` domain skill. Added to all skill tables. → `.claude/skills/manage-project/SKILL.md`, `CLAUDE.md`, `app/overview.md`, `reference/system-status.md`
7. **app/startup.md** — Created with managed project, friction log, and feedback log status checks. Added to overview hierarchy and index. → `app/startup.md`, `app/overview.md`
8. **installed-packages.md** — Referenced in overview's improvement pipeline section via extension packages note. → `app/overview.md`
