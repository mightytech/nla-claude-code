# Architecture Review: nla-claude-code

**Date:** 2026-06-05

Run after a substantial framework-update session (sibling-dirs → packages/ migration,
seven new framework skill wrappers, voice-and-values split, CLAUDE.md Execution
Principles refresh, Where Things Live structure record). Purpose: catch coherence
issues between docs that survived the structural changes.

## Document Chain

**Startup-time load** (loaded once per session, before any task):
- `CLAUDE.md` (auto-loaded by Claude Code)
- Framework startup via `/startup` → `packages/nla-framework/core/skills/startup.md`
  - which loads `packages/nla-framework/core/nla-foundations.md`
  - which loads `app/overview.md` (this project)
  - which loads `app/shared/values.md` (per the 2026-02-22 split: values are startup-loaded infrastructure)
- `app/startup.md` (app-specific initialization — status checks)
- `config.md` if present (not present in this project)

**Task-time load (setup-project):**
- `app/setup-project.md`
- prereqs: `app/shared/voice.md`, `app/shared/common-patterns.md`, `app/shared/deposit-templates.md`

**Task-time load (manage-project):**
- `app/manage-project.md`
- prereqs: `app/shared/voice.md`, `app/shared/common-patterns.md`, `reference/managed-projects.md`, conditional `app/shared/deposit-templates.md`

**Maintenance mode:**
- `packages/nla-framework/core/skills/maintain.md` (the present skill)
- `reference/design-rationale.md`, `reference/friction-log.md`, `reference/feedback-log.md`, most recent `reference/sessions/*`

## Findings

### Fix

*(none — nothing surveyed will cause incorrect behavior)*

### Improve

- **`CLAUDE.md:47` Session Initialization line is stale after the voice-and-values split.** The text reads "It loads foundational context — shared docs, voice, patterns — so you have full awareness…" That listing predates the split: `values.md` is now the startup-loaded infrastructure (per `install/structure-intent.md` and the 2026-02-22 update note), and `voice.md` is task-level. The current wording silently demotes values out of the startup-load mental model. Suggested phrasing: "shared values, voice, and patterns" — names what's actually loaded. — Cross-reference integrity / consistency.

- **`app/overview.md` carries three overlapping representations of `app/`:** Where Things Live (lines 110–140, added this session), Document Hierarchy (lines 219–233, pre-existing tree), and Document Index (lines 235–245, pre-existing flat list with links). All three list the same files. The pre-existing two were appropriate when overview.md had only the high-level map; Where Things Live now does that work and more (attribution, project-wide scope). Two of these earn their place — at most. Recommendation: drop the Document Hierarchy section entirely (its tree duplicates the `app/` portion of Where Things Live), keep Document Index because its bracketed link form has scan value the prose tables don't. — Orphaned / redundant content.

- **`CLAUDE.md` "What NOT to Do" (lines 105–111) and `app/shared/values.md` "Non-Negotiables" (lines 30–37) describe overlapping constraints without cross-referencing.** Both name "don't modify source code in managed projects" and "don't deposit without approval." Values.md frames them as Non-Negotiables (stronger); CLAUDE.md frames them as default-mode guardrails. Neither references the other. The split would be clearer if CLAUDE.md's section opened with a line like "These are operational guardrails — see also `app/shared/values.md` Non-Negotiables for the underlying commitments." Otherwise a maintainer editing one won't notice the other. — Consistency.

- **`CLAUDE.md` Environment table treats `app/shared/` as a generic entry**, hiding the load-order distinction that the 2026-02-22 split introduced (values at startup, voice at task time). A table is the right place to surface this — it's the runtime map. Consider replacing the single `app/shared/` row with two rows: `app/shared/values.md` (loaded at startup) and `app/shared/voice.md` (task-level prerequisite), keeping the directory-level row for `common-patterns.md` and `deposit-templates.md`. Or: keep the directory row and add one sentence above the table noting the load split. — Cross-reference integrity / consistency.

### Note

- **`reference/managed-projects.md` carries a stale path inside the AMG Source note** (`Penny post skills deposited (path: ../nla-penny-post/ from project)`). Already documented in the session log as "downstream divergence" — the deposited wrappers in `../test-nla-claude-code/` still point at the workspace sibling rather than `packages/nla-penny-post/`. This is a runtime correctness question for that managed project, not a coherence issue inside this NLA. Surfacing here for completeness.

- **`app/shared/deposit-templates.md:263` example path is structurally complex.** `(e.g., '../../nla-claude-code/packages/nla-penny-post')` is correct from a managed project at `../some-project/`, but reads as a riddle without re-deriving the path arithmetic. Optional improvement: add one sentence framing the calculation — "from a managed project at `../some-project/`, the resolved path is `../../nla-claude-code/packages/nla-penny-post`" — so the example is self-explaining.

- **`app/overview.md:8` ("This NLA operates on code projects from the outside")** uses sibling-dir framing implicitly. Post-migration, the framework dependencies are *inside* this project at `packages/`, but the project-management still happens outside the managed projects under `../`. Worth re-reading once to confirm nothing in the narrative implies cross-directory deposit reads of the framework itself.

## Summary

7 findings: 0 fix, 4 improve, 3 note. Overall the document chain survived the structural
changes cleanly — wrappers, paths, and skills tables are coherent. The four improve
findings cluster around one theme: **the voice-and-values split and the Where Things Live
addition need a few small surface fixes in CLAUDE.md and overview.md to fully land**.
None of the findings is a structural error; they're polishing items that keep the new
shape coherent for future readers and edits.
