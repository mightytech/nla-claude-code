# App Startup

After foundational context is loaded, check the NLA's current state and present a brief summary.

---

## Status Checks

1. **Managed projects** — Read `reference/managed-projects.md`. Count how many projects are registered. If none, note that `/setup-project` is the natural starting point.

2. **Friction log** — Read `reference/friction-log.md`. Count pending entries (entries without a resolved status). These are observations about the NLA waiting to be processed via `/maintain`.

3. **Feedback log** — Read `reference/feedback-log.md`. Count pending entries. These are external feedback items waiting to be processed via `/maintain`.

## Present Summary

After checking, present a brief status line:

- "[N] managed project(s). [X] friction log entries pending, [Y] feedback items pending."
- If nothing is pending: "No pending items."
- If no projects are managed: "No projects managed yet. Run `/setup-project` to add one."

Keep it to one or two lines. The developer is about to tell you what they want to do — don't make them scroll past a wall of status.
