# Maintenance Session: Framework Update — 0fc339b → 945f533

**Date:** 2026-06-03
**Status:** In Progress

## Intent

Bring this project current with the framework after ~3.5 months of dormancy. Apply
the seven `/update` items the framework's `update-notes.md` calls for: the
packages/ migration (foundational), six new skills (`/think`, `/debrief`, `/export`,
`/check-updates`, `/close`, `/guide`), the voice-and-values split, permissions
refresh, and optional wording/structure-record additions. End in a current state
the next session can build from.

## Changes Made

- **packages/ migration (2026-06-05).** Added framework and penny-post as in-project git submodules at `packages/nla-framework/` (pinned to v0.0.12, commit `c3e3e08`) and `packages/nla-penny-post/` (pinned to v0.0.1, commit `1ef501e`). Rewrote all 9 thin-wrapper paths via a single sed pass. Updated `CLAUDE.md` Environment table, `README.md` (prereqs, directory tree, framework-updates section), `app/config-spec.md` (framework default path), `app/shared/deposit-templates.md` (penny-post deposit path example), `reference/installed-packages.md` (Source paths). Logged the decision in `reference/design-rationale.md`.
- **Seven new framework skill wrappers (2026-06-05).** Added thin wrappers for `/check-updates`, `/think`, `/debrief`, `/close`, `/session-checkpoint`, `/guide`, `/export`. Updated skills tables in `CLAUDE.md`, `app/overview.md`, and `reference/system-status.md` (also refreshed system-status "Last updated" and Recent Changes). `/session-checkpoint` was a discovery — it ships in framework `install/skills-intent.md` without a dedicated update-note entry; the user opted to include it.
- **Split `voice-and-values.md` into `values.md` + `voice.md` (2026-06-05).** Per framework note 2026-02-22. Values (Transparency/Minimalism/Sovereignty) plus a Non-Negotiables section now live in `app/shared/values.md` — startup-loaded infrastructure. Voice (Direct/Technical/Practical/Honest + Editorial Standards) lives in `app/shared/voice.md` as a task-level prerequisite. Updated prerequisites in `setup-project.md` and `manage-project.md`, the document hierarchy + index in `app/overview.md`, and the directory tree + customization table in `README.md`. Removed the old combined file.
- **Pruned `.claude/settings.local.json` (2026-06-05).** Replaced ~35 accumulated session-specific `Bash(git -C ...)` entries (and now-redundant cross-dir paths to the old sibling directories) with the canonical declared minimum: `Bash(git:*)`, `Bash(ls:*)`, `Bash(test:*)` (framework manifest) + `Bash(gh:*)` (penny-post manifest), plus `Read(//home/container-user/workspace/**)` for managed-project access. File is gitignored, so the prune is local hygiene.
- **CLAUDE.md Execution Principles wording (2026-06-05).** Picked up framework refinements: renamed "Documentation is source code" → "NLA documents are source code" (per note 2026-04-18) with expanded body ("an ambiguous instruction is a bug; a missing section is a missing feature"); inserted new "Default to prose for design conversations" bullet (per note 2026-05-11) between the cardinal rule and flag-uncertainty.
- **"Where Things Live" section in `app/overview.md` (2026-06-05).** Adopted the Structure Decisions Protocol (framework note 2026-05-07). New section before the existing "Document Hierarchy" — full project tree, attribution tables per top-level area (top-level files, `app/`, `.claude/skills/`, `reference/`, `packages/`, `lib/`), and a Decision Sources scan table. Each entry is `[framework default]` or `[domain decision]` so future placement decisions have a consultation target.
- **Structural validation + install-log update (2026-06-05).** Ran `core/skills/validate-structural.md` checks inline: every wrapper target exists, all three skills tables (CLAUDE.md, overview.md, system-status.md) carry the same 19 skills, submodules pinned at tags, `app/` document hierarchy and filesystem match, README directory tree matches reality. All checks green. Appended Updated records to both `NLA Framework` and `Penny Post` sections in `reference/installed-packages.md` with package state, per-intent-file changes, and notes (including the deferred `reference/managed-projects.md` re-deposit cleanup).
- **Architecture + coherence review + six fix-now edits (2026-06-05).** Architecture review (`reference/sessions/2026-06-05-architecture-review.md`): 0 fix / 4 improve / 3 note — all four improve items clustered around the voice-and-values split and Where Things Live addition not having fully landed in CLAUDE.md / overview.md. Coherence review: 2 improve — CLAUDE.md double-framing (Grounding opener + first Execution Principle both saying "documents as source code"), and `values.md` "Who We Are" near-duplicating CLAUDE.md's opener. Fix-now batch (six edits): CLAUDE.md Session Initialization now names `values.md`, `overview.md`, framework foundations, and `startup.md` explicitly; CLAUDE.md Environment table now has separate rows for `values.md` (startup) and `voice.md` (task-level); CLAUDE.md "What NOT to Do" gains a one-line cross-reference to `values.md` Non-Negotiables; CLAUDE.md Grounding opener tightened to identity-only (operational framing now lives uniquely in Execution Principles); CLAUDE.md Grounding "fix is better writing, not better code" removed (covered by Execution Principles); `app/overview.md` Document Hierarchy block removed (Where Things Live now covers project-wide structure; Document Index retained for scannable link list); `values.md` "Who We Are" tightened to a half-sentence framing of the values that follow.

## Decisions Made

- **Pin at tagged releases**, not HEAD. The 2-3 commits past each tag are session-log finalizations; tagged releases are the explicit consumer release markers.
- **HTTPS submodule URLs**, matching framework `/create-app` and update-note conventions over the local SSH alias.
- **Don't disturb the user's in-progress edit to `reference/managed-projects.md`** (registers AMG Source as a managed project). Flagged downstream divergence: that managed project's deposited penny-post wrappers point at `../nla-penny-post/` (the workspace sibling), not at this NLA's new `packages/nla-penny-post/`. Re-deposit may be wanted at some point; not in scope for this session.

## What Didn't Work

(populated as work proceeds)

## Friction Log Entries Processed

None — the friction log is empty.

## Debrief

(captured at session close)

## State at Close

(captured at session close)
