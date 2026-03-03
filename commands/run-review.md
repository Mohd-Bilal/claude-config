---
description: Run the independent Claude code reviewer on the current branch. Can be invoked standalone without running the full workflow. Usage: /run-review
allowed-tools: Read, Grep, Glob, Bash(git diff:*), Bash(git log:*)
---

# Run Code Review

Invoke the independent code reviewer on the current implementation.

## Pre-flight checks

Before invoking the reviewer, verify:

1. `docs/Requirements.MD` exists — if not, stop and tell the human
2. `docs/Plan.MD` exists — if not, stop and tell the human
3. `tests/acceptance/` exists and has tests — if not, stop and tell the human
4. All acceptance tests are passing — run them now:
   - If any fail, stop and tell the human which tests are failing
   - Do not run the reviewer against a failing implementation

## If all checks pass

Invoke `/code-reviewer` as a forked subagent. It will:
- Read all the context files
- Review the implementation diff
- Write `docs/review-report.MD`

Once complete, print the contents of `docs/review-report.MD` in full
so the human can read the report directly in the terminal.

Then ask: "Would you like to proceed to the human PR review stage?"
