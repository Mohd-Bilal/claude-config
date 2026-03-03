# Global Claude Code Configuration

This file applies to every Claude Code session across all projects.

---

## Ticket Workflow

When working on any feature, bug, or task, follow the structured workflow
defined below. This workflow is available globally via slash commands and
skills in `~/.claude/`.

### When to invoke the workflow
- Starting work on any new feature or bug fix → `/start-ticket`
- Resuming interrupted work → `/resume-ticket`
- Running a standalone code review → `/run-review`

### Workflow overview

```
/start-ticket [PROJ-123 | free text | no args]
      ↓
/requirements-clarifier     ← HUMAN BLOCKED: full clarification loop
      ↓
Generate Test Suite          ← Claude agent, from Requirements.MD
      ↓
Human reviews test suite     ← HUMAN GATE
      ↓
Explore 2-3 solutions        ← Claude agent, parallel docs
      ↓
/solution-reviewer           ← HUMAN GATE: comparison + decision record
      ↓
Plan.MD                      ← Claude agent
      ↓
Implement                    ← Claude agent
      ↓
Run acceptance tests         ← auto, loop back on failure
      ↓
/code-reviewer               ← forked Claude instance, no shared context
      ↓
Human PR Review              ← HUMAN GATE: with review-report.MD as input
      ↓
Update Portfolio + JIRA      ← parallel
      ↓
STOP
```

### Human gates — non-negotiable
These steps are fully blocking. Never skip or timeout:
1. **Clarify** — `/requirements-clarifier` blocks until human confirms
2. **Test suite review** — human must approve before implementation
3. **Solution selection** — `/solution-reviewer` blocks until human picks one
4. **PR review** — human reviews Claude report + diff before merge

---

## Key Docs (generated per project/ticket)

| File | Purpose |
|------|---------|
| `docs/Requirements.MD` | Agreed requirements — source of truth |
| `docs/Plan.MD` | Implementation plan |
| `tests/acceptance/` | Test suite generated from requirements |
| `docs/solutions/` | One doc per solution approach |
| `docs/decisions/solution-decision.MD` | Recorded solution decision |
| `docs/review-report.MD` | Claude reviewer output |

---

## Global Rules

These apply in every session, every project:

- **Never skip a human gate.** If in doubt, pause and ask.
- **Never modify acceptance tests during implementation.** They are the contract.
- **Write operations are single-threaded.** No parallel file edits.
- **Use subagents for heavy reads.** Keep the main context lean.
- **Document deviations.** If you deviate from Plan.MD, update it first.
- **The clarification log is mandatory.** Always written by `/requirements-clarifier`.
- **The decision record is mandatory.** Always written by `/solution-reviewer`.

---

## Available Skills & Commands

### Slash Commands
| Command | Usage |
|---------|-------|
| `/start-ticket` | Start workflow — JIRA ID, free text, or no args |
| `/resume-ticket` | Resume interrupted workflow |
| `/run-review` | Run Claude code reviewer standalone |

### Skills (auto-invoked or via slash command)
| Skill | Role |
|-------|------|
| `/requirements-clarifier` | Structured clarification → Requirements.MD |
| `/solution-reviewer` | Solution comparison + decision recording |
| `/code-reviewer` | Independent review → review-report.MD (forked) |
