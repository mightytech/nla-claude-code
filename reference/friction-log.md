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

## Patterns to Watch

- **Deposit drift** — deposited files diverging from templates in ways that cause problems
- **Convention quality** — are generated conventions specific enough to be useful?
- **Import fidelity** — does existing CLAUDE.md content survive the import process intact?
- **Setup flow** — is the first-time setup conversation smooth or confusing?
