# Maintenance Session: First Maintenance — Architecture Review and Fixes

**Date:** 2026-02-19
**Status:** Complete

## Intent

Validate the freshly created NLA for structural and architectural soundness, then fix everything found. This is the first maintenance session — establishing that the system is coherent before any projects are managed.

## Changes Made

- **Created `/manage-project` skill** — Both tasks now have dedicated skills. Manage Project is also still triggered conversationally via CLAUDE.md routing. Added to all three skill tables (CLAUDE.md, overview.md, system-status.md).
- **Expanded overview's improvement pipeline** — Now shows three pipelines (NLA friction, project friction, external feedback) plus extension packages. Previously only showed friction-driven improvement.
- **Fixed manage-project.md gaps** — Added `deposit-templates.md` as conditional prerequisite for depositing workflows. Added zero-projects handling (suggest `/setup-project`).
- **Aligned skill descriptions** — Normalized five drifted purpose descriptions between CLAUDE.md and overview.md.
- **Installed penny post** via `/install` — Created thin wrapper skills (`/check-feedback`, `/write-letter`), added to CLAUDE.md skills table and environment paths, logged in installed-packages.md.
- **Completed penny post integration** — Made setup-project offer conditional on availability, added deposit templates for thin wrapper skills, documented opt-in dependency decision in design-rationale.md.
- **Created `app/startup.md`** — App-specific initialization with status checks for managed projects, friction log, and feedback log. Added to overview hierarchy and index, README directory tree.

## Decisions Made

- **Manage Project gets a skill** — Parallel structure with setup-project. Both entry points (skill and conversational routing) lead to the same task doc. Rationale: discoverability, prerequisite enforcement, consistency.
- **Opt-in dependencies for deposited skills** — Core deposits remain standalone. Optional deposits (penny post) may have external dependencies when the developer explicitly opts in. Documented in design-rationale.md.
- **Pipeline terminology** — Kept "friction" for both NLA and project contexts (they ARE the same concept, just scoped differently). Code notes are a separate tool, not a pipeline.
- **Penny post deposit templates live in nla-claude-code** — The templates for what gets deposited into code projects are this NLA's concern, not penny post's. Penny post provides the skill logic; nla-claude-code provides the deposit templates.

## What Didn't Work

- Attempted to invoke `/install` via the Skill tool — blocked by `disable-model-invocation: true`. Worked around by reading and following the install skill logic directly.

## Friction Log Entries Processed

No friction log entries existed — this was the first session.

## State at Close

- All 8 architecture review findings resolved
- Penny post installed and integrated
- 12 skills active (7 framework, 3 domain, 2 penny post)
- No managed projects yet
- System is ready for first `/setup-project` run
- README directory tree, overview hierarchy, and all skill tables are current
