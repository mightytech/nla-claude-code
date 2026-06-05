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
