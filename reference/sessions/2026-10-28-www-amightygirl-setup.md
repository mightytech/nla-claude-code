# Session: www.amightygirl.com Setup + Process Helpers Install

**Date:** 2026-10-28
**Status:** Complete

## Intent

First real use of this NLA: set up www.amightygirl.com (legacy Magento 1.9 store) as a managed project, replacing a pre-NLA, rule-heavy CLAUDE.md with intent-first configuration. Process helpers was installed along the way so its skills could be deposited too.

## Changes Made

**In this NLA**
- Installed process helpers (`packages/nla-process-helpers/`, pinned v0.0.1) with thin wrappers for `/unpack`, `/brainstorm-cluster`, `/steelman`, `/devils-advocate`. CLAUDE.md, the overview structure record, README, system status, and the install log updated together. (`0096205`)
- Registered www.amightygirl.com in `reference/managed-projects.md` — the first managed project. (`8ec2ad0`)
- Logged six friction entries, all `setup-project` or general: imported config isn't verified; deposit paths ignore git/deploy; untracked files get overwritten without backup; only penny post is offered as a package deposit; the default-mode guardrail contradicts setup/install edits; decisions were presented as menus instead of recommendations. (`b327362` + this commit)

**In www.amightygirl.com** (all under paths its `.gitignore` already excludes — nothing reaches git or production)
- `CLAUDE.md` rewritten as a 51-line router: posture (legacy store, keep it running, OpenMage LTS upgrade only when asked), environment (Claude runs inside the dev VM; run PHP freely, ask before anything with effects beyond the VM), git.
- `.claude/docs/conventions.md`: where code goes, theme, build, PHP, verifying changes, giveaways, WordPress, dependencies.
- Skills: standalone `/friction-log`, `/code-note`; thin wrappers for penny post and process helpers pointing at `../nla-claude-code/packages/`.
- Logs at `.claude/reference/` (not `reference/`, to avoid editing the tracked `.gitignore`).
- Original CLAUDE.md preserved at `.claude/reference/CLAUDE.md.pre-nla-2025-07-03`.

## Decisions Made

- **Claude may run PHP/Magento commands in the dev VM.** The old ban assumed Claude ran on the Mac; it now runs in the VM. Limit is outward reach (email, cron/newsletter, external APIs, bulk writes), not execution.
- **Claude config stays out of git** for this project. Git pull is the deploy mechanism; history comes from nightly disk backups. Developer will revisit at the OpenMage upgrade.
- **`/check-feedback` deposited despite having no intake channel** (repo is on Bitbucket) — may motivate a non-GitHub mailbox for penny post.
- **Friction log, not a letter, for this NLA's own gaps.** Same project, maintained on another machine — git carries the friction log there; letters are for cross-project feedback.

## Debrief

Ran `/debrief`. Refined conclusions, agreed with the developer:

- **Verification carried the setup.** Checking the old config against the machine (hostname, `which php`, the gulpfile, `local.xml`) found three wrong claims and that `build/` output is tracked in git. The task doc doesn't ask for any of it. → friction log.
- **Posture first worked.** Writing the one-paragraph "how to work here" before anything else set the level; once the developer confirmed it, both files followed and were approved unchanged.
- **Lead with recommendations.** The developer twice asked "what's your read?" after a menu of options; things sped up once recommendations came first. → friction log (voice).
- **The default-mode guardrail is too broad** — it forbids record-keeping and `/install` edits the tasks require. → friction log.
- **Tag check only fires inside `/close` and `/maintain`** — a mid-session push skipped it. → letter to framework (below).
- **Nested process-helpers copy in the framework trails its tag** with stale sibling-path intents; nearly synthesized from it. → letter to framework (below).
- **Unverified:** whether the deposited package-skill wrappers run correctly from a www.amightygirl.com session (relative paths, permission prompts). First use will tell.

## Unsent Letter: nla-framework

`gh` isn't installed on the dev VM, so this couldn't be submitted. File it as an issue on `mightytech/nla-framework` from the maintenance machine.

**Title:** Shippability tag check only fires inside /close and /maintain; nested process-helpers pin trails its tag

### Source & context

From nla-claude-code (a domain NLA that manages Claude Code configuration in traditional code projects), on framework v0.0.12. Written at the end of a default-mode session: the NLA's first `/setup-project` run, which also installed process helpers via `/install`. Two framework-level observations came out of the debrief.

### Items

#### 1. Pushes outside /close and /maintain skip the Shippability tag check

**Confidence:** high that it happened and why; moderate on the best fix.

Mid-session, the developer said to commit and push. I did — three commits, one of them consumer-facing (process helpers install: `CLAUDE.md`, `.claude/skills/`, `app/overview.md`). No tag. The miss only surfaced later, when `/close` loaded `close.md`, which says the rule "attaches tags to *push moments*, not commits."

The instruction chain: the Shippability rule lives in `core/skills/maintain.md` ("Shippability at Commit Time") and is applied in `core/skills/close.md` step 5. Neither skill was loaded when the push happened. Nothing loaded at startup (`nla-foundations.md`, the domain `CLAUDE.md`) mentions tagging. So the rule is scoped to *skills* while its own framing scopes it to *push moments* — and push moments happen anywhere.

**Suggestion:** a one-line principle in something loaded at startup — `nla-foundations.md` or the CLAUDE.md intent — along the lines of: "Before any push, apply the Shippability tag check (see `core/skills/maintain.md`)." The full rule can stay where it is; the trigger needs to be reachable from wherever a push happens.

#### 2. The framework's nested process-helpers submodule is pinned behind its tag, with stale install intents

**Confidence:** high on the facts as of framework v0.0.12; I haven't checked whether a later framework release moved the pin.

In framework v0.0.12, `packages/nla-process-helpers` is pinned at `e091477` (`v0.0.1~3`). That copy's `install/install.md` still lists "This repo cloned as a sibling — `../nla-process-helpers/`" as a prerequisite, and `skills-intent.md` points wrappers at `../nla-process-helpers/app/…`. The process-helpers v0.0.1 tag already uses `packages/nla-process-helpers/`.

Before running `/install`, I read the nested copy to understand the package and almost synthesized wrappers from the sibling-path intents. I caught it only by re-reading after `git submodule add` pulled the real v0.0.1.

**Suggestion:** advance the nested pin to the tag. More generally, any consumer browsing `packages/nla-framework/packages/` sees whatever the framework pinned, so keeping those pins at tags avoids this for every package.

### Relationships

Independent items. Both are about version state being invisible at the moment it matters — one at push time, one at install time.

---
*Drafted with /write-letter from [nla-claude-code](https://github.com/mightytech/nla-claude-code) during a default-mode session.*

## State at Close

**Working**
- www.amightygirl.com is managed and its config is live locally. Process helpers is installed in this NLA.

**Context for next time**
- The maintenance machine sees all of this after a pull; `/startup` will report 6 pending friction entries.
- Open question for www.amightygirl.com: is the dev DB a production copy with real customer emails, and does dev SMTP send? If dev mail is blackholed, loosen the email part of its "ask first" rule.
- The www.amightygirl.com Claude config isn't in git — only the nightly disk backup protects it.

**Decisions awaiting implementation**
- File the framework letter above (`mightytech/nla-framework`).
- `/maintain` session on the six friction entries — mostly `app/setup-project.md`, `app/shared/deposit-templates.md`, `common-patterns.md` ("Import Before Overwrite"), `voice.md`, and CLAUDE.md's default-mode guardrail. The backup-before-overwrite entry may also warrant a framework letter.

**Where to pick up**
- Use Claude Code in www.amightygirl.com; `/friction-log` there, bring entries back via `/manage-project`.
