# Common Patterns

Recurring patterns the NLA should recognize. Starting minimal — these grow through `/friction-log` + `/maintain` iteration.

---

## 1. Import Before Overwrite

**What to look for:** A code project that already has a CLAUDE.md or `.claude/` directory with existing content.

**What to do:** Read and understand what's there before depositing anything. Incorporate existing conventions into the new structure. The developer chose those conventions for reasons — preserve the intent even if you reorganize the format.

**When NOT to apply:** When the developer explicitly says "start fresh" or "ignore the existing config."

## 2. Router Over Monolith

**What to look for:** A CLAUDE.md that's getting long, or a project with distinct concerns (language conventions, testing patterns, deployment rules).

**What to do:** Structure CLAUDE.md as a router that points to focused documents in `.claude/docs/`. Each doc handles one concern. The router loads the right context based on what the developer is doing.

**When NOT to apply:** Small projects with simple needs. A 30-line CLAUDE.md doesn't need routing. Don't add structure for structure's sake.

## 3. Convention Docs Explain Why

**What to look for:** Convention docs that only list rules ("use snake_case", "prefer composition").

**What to do:** Add the reasoning. "Use snake_case because this codebase follows PEP 8 and consistency reduces cognitive load during review." Purpose enables judgment in edge cases.

**When NOT to apply:** When the convention is genuinely universal and self-evident (e.g., "don't commit secrets").

## 4. Deposit Minimally, Iterate Forward

**What to look for:** The urge to deposit comprehensive configuration on first setup.

**What to do:** Deposit the minimum that's useful — a router CLAUDE.md, a few core conventions, the friction-log skill. The developer uses it, notices what's missing, logs friction, and comes back to the NLA to add more. This produces better configuration than guessing upfront.

**When NOT to apply:** When the developer has clear, detailed requirements and knows exactly what they want. Don't force iteration when they've already iterated in their head.
