# Installed Packages

Record of NLA packages installed in this project. Maintained by `/install` and `/update`.

---

## NLA Framework

- **Installed:** 2026-02-19
- **State at install:** commit `0fc339b` (2026-02-19)
- **What was done:** Initial project creation via `/create-app`. Framework provides core skill logic (startup, maintain, friction-log, validate, preferences, install, update) via thin wrappers.
- **Updates:**
  [None yet — run `/update` to check for framework changes]

## Penny Post

**Source:** `../nla-penny-post/`
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
