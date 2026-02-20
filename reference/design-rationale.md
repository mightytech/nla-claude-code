# Design Rationale

For maintainers. Records why this NLA is built the way it is.

---

## Why an NLA?

CLAUDE.md files are natural language — they're instructions written in prose for an LLM to follow. Managing them is fundamentally a natural language task: understanding what a developer wants, translating that into conventions Claude Code will follow, and iterating based on observed behavior.

Traditional tools (linters, config generators, templates) can produce CLAUDE.md files, but they can't understand nuance: "I want Claude to be more conservative with refactoring" isn't a setting you can toggle. An NLA can have that conversation, understand the intent, and write conventions that capture it.

## Why This Structure

### External NLA, Deposited Files

The NLA lives outside the code projects it manages. This separates the tool (this NLA) from its output (deposited config files). Benefits:

- Code projects stay clean — no NLA runtime files in the codebase
- Deposited files work standalone — developers don't need the NLA to benefit
- One NLA manages multiple projects — conventions can be consistent or project-specific
- The NLA can be versioned independently of any code project

### Router Pattern for CLAUDE.md

Deposited CLAUDE.md files use a router pattern — a short top-level file that points to focused convention docs in `.claude/docs/`. This keeps CLAUDE.md scannable and allows conventions to grow without the file becoming unwieldy.

Alternative considered: monolithic CLAUDE.md. Rejected because it doesn't scale — a 200-line CLAUDE.md is hard to maintain and hard for Claude to prioritize.

### Standalone Deposits

Deposited skills and docs don't reference this NLA or the framework. They work on their own in any Claude Code session. This means:

- Developers without the NLA still benefit
- One developer can improve config for the whole team
- No runtime dependency on the NLA being present

Alternative considered: thin wrappers back to the NLA. Rejected because code projects can be anywhere on the filesystem, and creating a runtime dependency on an external NLA would be fragile.

### Two Friction Logs

The code project has its own friction log (about Claude Code behavior) separate from this NLA's friction log (about the NLA itself). Same pattern, different contexts:

- Code project friction → feeds into convention improvements via this NLA
- NLA friction → feeds into NLA improvements via `/maintain`

### Code Notes as a Deposit

Code notes (`/code-note`) demonstrate that this NLA deposits capabilities, not just configuration. It's a lightweight, LLM-native tool that works with codebase context. This establishes the pattern for future depositable capabilities.

## Key Design Decisions

### Import Before Overwrite

**Decision:** Always scan and import existing CLAUDE.md content before depositing.

**Why:** Developers choose their conventions for reasons. Discarding existing config loses that knowledge. Even if we restructure the format, the content should be preserved.

**Alternative:** Start fresh every time. Rejected because it disrespects existing work and loses project-specific knowledge.

### Deposit Minimally

**Decision:** Start with minimal conventions and iterate forward.

**Why:** A small, correct configuration beats a comprehensive, wrong one. Developers know their projects better than the NLA can guess. Better to deposit a foundation and let friction-driven improvement add what's needed.

**Alternative:** Generate comprehensive conventions upfront. Rejected because generic conventions often don't fit specific projects, creating more friction than they prevent.

### Penny Post as Optional

**Decision:** Penny post integration is offered during setup, not included by default. The offer is conditional — only shown when penny post is actually installed in this NLA.

**Why:** Not every project needs GitHub issue triage. Solo projects especially may not. Offering it as an option keeps the base deposit clean while making the capability available. Making the offer conditional on availability prevents referencing something that doesn't exist.

### Opt-in Dependencies for Deposited Skills

**Decision:** Core deposits (friction-log, code-note) are standalone — they work without any external dependencies. Optional deposits like penny post skills may have external dependencies when the developer opts in.

**Why:** Penny post skills need penny post's logic to function — you can't make GitHub issue triage standalone in a meaningful way. The developer is told what the dependency is, they decide whether to accept it, and if they say yes, the thin wrappers go in. The NLA resolves paths at deposit time. This preserves the standalone principle for the base experience while allowing richer capabilities for developers who want them.

**Alternative:** Make all deposits standalone (copy penny post logic into each project). Rejected because it would create duplicated logic that drifts out of sync, and updating penny post would require re-depositing to every project.

**Affects:** `app/setup-project.md` (conditional offer), `app/shared/deposit-templates.md` (thin wrapper templates), deposited skill files in code projects.

## Adding Decisions

When making significant design choices during `/maintain`, add them here:

```
### [Decision Title]

**Decision:** What was decided.
**Why:** The reasoning.
**Alternative:** What was considered and rejected.
**Affects:** What this decision impacts.
```
