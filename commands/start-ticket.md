---
description: Start the full workflow for a ticket. Pass a JIRA ticket ID (e.g. /start-ticket PROJ-123) OR pass no arguments and type out the requirements directly when prompted.
allowed-tools: Read, Write, Bash(git *), mcp__jira__*
---

# Start Ticket Workflow

Input: $ARGUMENTS

## Step 1 — Determine Input Mode

Look at `$ARGUMENTS`:

### Mode A — JIRA ticket ID provided (e.g. `PROJ-123`)
If `$ARGUMENTS` looks like a JIRA ticket ID (letters, dash, numbers):

1. Use the JIRA MCP tool to fetch the ticket — get the full description,
   acceptance criteria, and any linked tickets.
2. Print a summary to confirm you have the right one:
   - Title
   - Description (key points)
   - Acceptance criteria (numbered list)
3. Ask the human: "Is this the right ticket? Reply YES to continue."
4. Wait for confirmation, then invoke `/requirements-clarifier` with the
   ticket content as context.

### Mode B — No arguments provided
If `$ARGUMENTS` is empty:

1. Say to the human:
   ```
   No ticket ID provided. Please type out your requirements below.
   Include as much detail as you have — title, description, acceptance
   criteria, edge cases, anything relevant. Don't worry about formatting;
   I'll structure it during clarification.
   ```
2. Wait for the human to type their requirements.
3. Once received, invoke `/requirements-clarifier` with the
   human's typed input as context.

### Mode C — Requirements typed directly as arguments
If `$ARGUMENTS` is a long free-text description (not a ticket ID):

1. Confirm receipt:
   ```
   Got it — I'll use the requirements you've provided as the starting point.
   ```
2. Invoke `/requirements-clarifier` with `$ARGUMENTS` as the input context.

---

In all modes, do not proceed past `/requirements-clarifier` until the
human has explicitly confirmed the requirements summary.
