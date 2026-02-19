# Configuration Spec

What's configurable in nla-claude-code. This defines the options; actual preferences live in `config.md` (gitignored).

---

## What's Configurable

### Default Deposits

What gets deposited into code projects by default during `/setup-project`.

- **Core deposits** (always included): CLAUDE.md router, conventions.md, friction-log skill, code-note skill
- **Optional deposits** — which to offer during setup:
  - Penny post wrappers (default: ask during setup)
  - Additional convention docs (default: ask if project complexity warrants it)

### Managed Project Defaults

- **Default project path prefix** — if most of your projects are in the same directory, set a prefix to avoid typing full paths. Default: `../` (sibling directories).

### Convention Generation

- **Convention detail level** — how detailed generated conventions should be.
  - `minimal` — just the essentials, developer adds detail through iteration
  - `moderate` — reasonable coverage with explanations (default)
  - `comprehensive` — thorough coverage, more upfront guessing

### Communication Style

- **Verbosity** — how much the NLA explains during setup and management.
  - `concise` — minimal narration, just the essentials
  - `standard` — explain what you're doing and why (default)
  - `detailed` — thorough explanations, good for learning

### Framework Path

- **Framework location** — path to the NLA Framework. Default: `../nla-framework/`

## Constraints

These are NOT configurable:

- **The cardinal rule** — the developer decides. Always present plans before depositing.
- **Import before overwrite** — always scan existing config before depositing.
- **Standalone deposits** — deposited files must work without the NLA present.
- **Friction log format** — follows the framework standard for consistency.

## Guidance for the Config Conversation

When a developer runs `/preferences` for the first time:

- Start with managed project paths — that's the most immediately useful setting
- Convention detail level is the next most impactful choice
- Most developers are fine with defaults for everything else
- If they're unsure, suggest keeping defaults and adjusting after using the NLA for a while
