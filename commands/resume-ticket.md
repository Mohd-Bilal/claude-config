---
description: Resume an in-progress ticket workflow from where it was left off. Usage: /resume-ticket PROJ-123
allowed-tools: Read, Write, Bash(git *), mcp__jira__*
---

# Resume Ticket Workflow

Ticket ID: $ARGUMENTS

Resume the in-progress workflow for ticket: **$ARGUMENTS**

## Your first actions:

1. Read `docs/Requirements.MD` to understand the agreed requirements.
2. Read `docs/Plan.MD` if it exists, to understand the current plan.
3. Check `docs/review-report.MD` if it exists, to see if a review has been done.
4. Run `git status` and `git log main..HEAD --oneline` to understand current state.
5. Check test results: run the acceptance test suite in `tests/acceptance/`.

Based on what you find, determine which step of the workflow (from CLAUDE.md)
you are currently on, and resume from there. Summarise your findings to the
human before continuing:

- Current step
- What has been completed
- What is next
- Any blockers or open questions

Wait for the human to confirm before proceeding.
