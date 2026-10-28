# Managed Projects

Registry of code projects managed by this NLA. Updated by `/setup-project` when new projects are added, and during ongoing management as project state changes.

---

## How This Registry Works

Each managed project gets an entry with:
- **Path** — where the project lives on the filesystem
- **Language/Framework** — detected during setup
- **Date added** — when `/setup-project` was run
- **What was deposited** — which files and skills were placed
- **Notes** — any special considerations (existing config imported, penny post enabled, etc.)

When working on a managed project, read its entry here first to understand its state.

---

## Projects

### www.amightygirl.com

- **Path:** `../www.amightygirl.com` (sibling of this NLA)
- **Language/Framework:** PHP 7.3, Magento 1.9.4.5 (theme `amg/amightygirl` on `gravdept/acumen`), WordPress via Fishpig, Gulp 3.9.1 frontend build. Remote on Bitbucket.
- **Date added:** 2026-10-28
- **What was deposited:**
  - `CLAUDE.md` — router; intent-first posture (legacy store, keep it running, OpenMage LTS upgrade only when asked), environment, git
  - `.claude/docs/conventions.md` — where code goes, theme, build, PHP, verifying changes, giveaways, WordPress, dependencies
  - `.claude/skills/friction-log/`, `.claude/skills/code-note/` — standalone
  - `.claude/reference/friction-log.md`, `.claude/reference/code-notes.md`
  - Penny post wrappers `/check-feedback`, `/write-letter` → `../nla-claude-code/packages/nla-penny-post/app/`
  - Process helpers wrappers `/unpack`, `/brainstorm-cluster`, `/steelman`, `/devils-advocate` → `../nla-claude-code/packages/nla-process-helpers/app/`
- **Notes:**
  - **Nothing is in git.** The project's `.gitignore` already excludes `CLAUDE.md` and `.claude/`, and production deploys by pulling from git — so all Claude config stays local by design. That's why the logs live at `.claude/reference/` instead of the usual `reference/`: it avoided editing the tracked `.gitignore` (which would itself deploy). History comes from the nightly disk backup, not git. Developer plans to revisit this when the site is upgraded.
  - **Imported:** existing CLAUDE.md (2025-07-03, written before the NLA framework). Preserved at `.claude/reference/CLAUDE.md.pre-nla-2025-07-03`. Its environment premise was stale — Claude Code now runs inside the dev VM (hostname `dev.amightygirl.com`), not on the Mac — so the "never run PHP" ban became "run freely inside the VM; ask before anything with effects beyond it (email, cron/newsletter queue, external APIs, bulk writes)." Also corrected: Gulp source paths (`skin/frontend/gravdept/acumen/*/src/`, not `amg/amightygirl/src/`) and cache clearing (backend is Redis, so `var/cache/` deletion doesn't work).
  - **Open question:** whether the dev DB is a production copy with real customer emails, and whether dev SMTP actually sends. If dev mail is blackholed, the email part of the "ask first" rule can be relaxed.
  - `/check-feedback` has no intake channel (penny post reads GitHub issues; this repo is on Bitbucket). Deposited anyway at developer request — a possible driver for a non-GitHub mailbox. The wrapper says so and tells Claude to stop rather than improvise.
  - Penny post and process helpers wrappers depend on this NLA staying at `../nla-claude-code/`.
  - Node isn't installed in the VM; Gulp `build/` output is tracked in git, so frontend source changes need the developer to rebuild and commit.
