# Friction Log

Observations about how this NLA behaves — things that didn't work as expected, things that worked well, things worth watching. This is about the NLA itself, not about Claude Code behavior in managed projects (those observations live in each project's own friction log).

## How to Use This Log

Run `/friction-log` to add entries from any context. Entries are processed during `/maintain` sessions.

### Entry Types
- **output** — Something about what the NLA produced (deposited files, convention content)
- **process** — Something about how the NLA works (setup flow, management conversation)
- **documentation** — Something about the NLA's own docs (unclear, missing, contradictory)

### Severity
- **positive** — Something that worked well, worth preserving
- **minor** — Small issue, easy to address
- **moderate** — Notable issue, should be addressed
- **significant** — Serious issue, needs prompt attention

### Entry Format

#### YYYY-MM-DD: [Brief title]

- **Type:** output | process | documentation
- **Severity:** positive | minor | moderate | significant
- **Task:** setup-project | manage-project | general
- **Status:** open | investigating | resolved (YYYY-MM-DD: description)
- **Observation:** What happened
- **Expected:** What should have happened (if applicable)
- **Context:** What you were doing when you noticed
- **Proposed fix:** What might address this (if known)

Not all fields are required. Use what's relevant.

## Entries

[Newest first]

#### 2026-10-28: Setup offers penny post as an optional deposit, but not other installed packages

- **Type:** documentation
- **Severity:** minor
- **Task:** setup-project
- **Status:** open
- **Observation:** `app/setup-project.md` step 3 offers penny post skills when penny post is installed, but says nothing about other packages. The developer asked for process helpers in www.amightygirl.com; that turned out to require installing process helpers in this NLA first (it existed only nested inside the framework's submodule), then hand-writing wrappers with no template in `deposit-templates.md`.
- **Expected:** Setup checks `reference/installed-packages.md` and offers each installed package that provides skills, with a generic thin-wrapper template for deposited package skills.
- **Context:** First `/setup-project` run, www.amightygirl.com.
- **Proposed fix:** Generalize the penny post bullet in step 3 to "installed packages with skills," and turn the penny-post wrapper templates into a single package-wrapper pattern (path resolved at deposit time, external dependency noted in the registry).

#### 2026-10-28: Overwriting a CLAUDE.md that git doesn't track destroys the original

- **Type:** process
- **Severity:** moderate
- **Task:** setup-project
- **Status:** open
- **Observation:** www.amightygirl.com's existing CLAUDE.md was gitignored, so replacing it with the router would have left no copy anywhere but the nightly disk backup. I saved it to `.claude/reference/CLAUDE.md.pre-nla-2025-07-03` on my own judgment — nothing in the task asked for it.
- **Expected:** Before overwriting any existing file, setup checks whether version control holds a copy, and preserves the original when it doesn't.
- **Context:** Depositing the router CLAUDE.md over a pre-NLA one.
- **Proposed fix:** Add to step 5 (or to "Import Before Overwrite" in `common-patterns.md`): if a file being replaced isn't tracked, keep the original alongside the deposit and record where in the registry. Possibly framework-relevant — any NLA that deposits files has this risk; consider a letter upstream during `/maintain`.

#### 2026-10-28: Deposit locations ignore how the project tracks and deploys files

- **Type:** documentation
- **Severity:** moderate
- **Task:** setup-project
- **Status:** open
- **Observation:** `deposit-templates.md` puts the friction log and code notes at `reference/` in the project root. In www.amightygirl.com, `.gitignore` already excludes `CLAUDE.md` and `.claude/` but not `reference/`, and production deploys by pulling from git — so the default location would have put Claude's logs on track to reach the production server. Ignoring `reference/` would have meant editing the tracked `.gitignore`, which itself deploys. We settled on `.claude/reference/`, but only because the developer and I worked through it in conversation.
- **Expected:** Setup asks (or detects) whether Claude config should be tracked in git, and how the project deploys, before choosing deposit paths.
- **Context:** Planning the deposit for a legacy site where git is the deploy mechanism.
- **Proposed fix:** Add a scan item to step 2 — read `.gitignore` for Claude-related entries and ask about deployment — and make the log location a deposit-time choice (`reference/` when tracking is wanted, `.claude/reference/` when everything stays local). Deposited skills then point at whichever path was chosen.

#### 2026-10-28: Setup imports existing config without checking it against reality

- **Type:** process
- **Severity:** moderate
- **Task:** setup-project
- **Status:** open
- **Observation:** "Import Before Overwrite" told me to preserve the existing CLAUDE.md's intent, but nothing told me to verify its claims. Three were wrong: it said Claude Code runs on a Mac and must never execute PHP (Claude Code now runs inside the dev VM, with PHP available); it gave Gulp source paths that don't exist; and its cache-clearing advice deletes `var/cache/` when the cache backend is Redis. I caught them only by checking the machine and the files on my own initiative. Carried over faithfully, they'd have kept Claude from running PHP for no reason and pointed it at files that don't exist.
- **Expected:** Import is "verify, then preserve intent": factual claims in existing config (environment, paths, commands, versions) are checked against the project and the runtime, and discrepancies are shown to the developer as decisions, not silently fixed or silently kept.
- **Context:** Scanning www.amightygirl.com's July 2025 CLAUDE.md, written before the NLA framework existed.
- **Proposed fix:** Extend step 2 of `setup-project.md` and the "Import Before Overwrite" pattern: verify factual claims where cheap (paths exist, tools are installed, config matches), and distinguish facts to check from preferences to preserve. Likely just as relevant for `manage-project.md`, since deposited config also drifts out of date.

## Patterns to Watch

- **Deposit drift** — deposited files diverging from templates in ways that cause problems
- **Convention quality** — are generated conventions specific enough to be useful?
- **Import fidelity** — does existing CLAUDE.md content survive the import process intact?
- **Setup flow** — is the first-time setup conversation smooth or confusing?
