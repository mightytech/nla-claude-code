# Installed Packages

Record of NLA packages installed in this project. Maintained by `/install` and `/update`.

---

## NLA Framework

**Source:** `packages/nla-framework/` (from https://github.com/mightytech/nla-framework.git)
- **Installed:** 2026-02-19
- **State at install:** commit `0fc339b` (2026-02-19)
- **What was done:** Initial project creation via `/create-app`. Framework provides core skill logic (startup, maintain, friction-log, validate, preferences, install, update) via thin wrappers.

### Updated 2026-06-05

**Package state:** v0.0.12 (commit `c3e3e08`) — pinned to tagged release; HEAD `945f533` was 2 commits past (session-log finalizations only).

| Intent File | What Changed | Changes Made |
|-------------|-------------|--------------|
| `install/install.md` | Sibling-directory model retired; consumers should live at `packages/<name>/` as submodules. Permissions section declares baseline `Bash(git:*)`, `Bash(ls:*)`, `Bash(test:*)`. | Added framework as `packages/nla-framework/` submodule pinned at v0.0.12. Rewrote all 9 wrapper paths and prose references in CLAUDE.md, README.md, app/config-spec.md, deposit-templates.md, installed-packages.md. Refreshed `.claude/settings.local.json` to the declared canonical set plus `Read(//home/container-user/workspace/**)`. |
| `install/skills-intent.md` | Seven new framework skills landed since install: `/think`, `/debrief`, `/export`, `/check-updates`, `/close`, `/session-checkpoint`, `/guide`. (`/unpack` moved to `nla-process-helpers/` — not installed here.) | Created thin wrappers for all seven. Added each to skills tables in CLAUDE.md, app/overview.md, and reference/system-status.md. |
| `install/CLAUDE-intent.md` | Renamed Execution Principle "Documentation is source code" → "NLA documents are source code" (2026-04-18) with expanded body. Added new principle "Default to prose for design conversations" (2026-05-11). | Applied both wording updates in CLAUDE.md's Execution Principles. |
| `install/structure-intent.md` | Split `voice-and-values.md` into `values.md` (startup-loaded infrastructure) + `voice.md` (task-level prerequisite). Adopted "Where Things Live" as the structure record (per Structure Decisions Protocol 2026-05-07). | Split `app/shared/voice-and-values.md` into `values.md` + `voice.md`; updated task-doc prereqs, overview index, README customization table. Added "Where Things Live" section to `app/overview.md` — full project tree with `[framework default]` / `[domain decision]` attribution per top-level area, plus Decision Sources scan table. |
| `install/package-intent.md` | Shippability convention added (consumer-facing vs internal at commit time). Tag cadence refined to per-push (2026-05-08). | No project-side change required — applies to package authoring, not consumption. Tag-at-push will inform `/close` behavior at session end. |
| `core/nla-foundations.md` | Many advances (NLA Shapes, Cardinal Rule reframe, Values Are Visible principle, multiple new Working Rhythms: Validation Flow, Structural Change Discipline, Inquiry Flow, Session-Bracketing Discipline, plus writing standards Section 2.6). | All auto-propagate via `packages/nla-framework/core/nla-foundations.md` loaded at startup. No project-side changes. |

**Notes:**
- Pinned at tagged release v0.0.12 (HEAD was at 945f533, 2 commits past — both session-log finalizations, not behavioral).
- `/unpack` was moved to `nla-process-helpers/` in 2026-02-22 update note; this project never installed it, so no removal needed.
- `/session-checkpoint` ships in `install/skills-intent.md` without a dedicated update-note entry; included at maintainer request.
- The user's in-progress edit to `reference/managed-projects.md` (registering AMG Source as a managed project) was left unmodified. That project's deposited penny-post wrappers point at `../nla-penny-post/` (the workspace sibling), not at this NLA's new `packages/nla-penny-post/`. They keep working as long as the sibling exists; re-depositing would align the managed project with the new layout but is not in scope for this update session.

## Penny Post

**Source:** `packages/nla-penny-post/` (from https://github.com/mightytech/nla-penny-post.git)
**Installed:** 2026-02-19
**Package state:** commit `9186c5a` (2026-02-19)

### What was done

| Intent File | Integration Point | Changes Made |
|-------------|------------------|--------------|
| `skills-intent.md` | `.claude/skills/` | Created thin wrapper skills: `/check-feedback` → `../nla-penny-post/app/check-feedback.md`, `/write-letter` → `../nla-penny-post/app/write-letter.md` |
| `CLAUDE-intent.md` | `CLAUDE.md` | Added `/check-feedback` and `/write-letter` to skills table. Added `../nla-penny-post/` to environment paths. |

### Notes

- Installed during a `/maintain` session while addressing architecture review findings about penny post integration.
- Feedback capabilities are additive — the NLA can now receive and triage feedback via `/check-feedback` and send feedback to other projects via `/write-letter`.
- Feedback processing happens in this NLA's session (full project context), not in penny post.
- Accepted feedback goes to `reference/feedback-log.md`, which already existed.

### Updated 2026-06-05

**Package state:** v0.0.1 (commit `1ef501e`) — pinned to tagged release; HEAD `6a5bba1` was 1 commit past (session-log finalization).

| Intent File | What Changed | Changes Made |
|-------------|-------------|--------------|
| `install/install.md` | Permissions section declares `Bash(gh:*)`. Notes that `Read(packages/nla-penny-post/**)` is not needed post-migration (in-project). | Added penny-post as `packages/nla-penny-post/` submodule pinned at v0.0.1. Updated deposit-templates.md example path to reflect new location. Refreshed wrapper paths for `/check-feedback` and `/write-letter`. `Bash(gh:*)` added to `.claude/settings.local.json`. |
| `install/skills-intent.md` | Updated for `packages/` paths. | Wrappers already in place; only path-rewrite needed. |
| `install/CLAUDE-intent.md` | Path updates. | Already reflected in CLAUDE.md Environment table. |

**Notes:** Pinned at tagged release v0.0.1 (HEAD was at 6a5bba1, 1 commit past — a session-log finalization, not behavioral).
