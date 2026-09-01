---
name: catch-me-up
description: Summarizes a stale session from its conversation history. It reports what blocks the session, the goal, the decisions, and the work left. Use when the user says "catch me up", "where were we", "what is this session about", "what's left", or returns to a session after a break.
---

# catch-me-up

The user lost the thread of this session. Rebuild it from the conversation history. Do not rerun work. Read a file only when the conversation created a plan, task list, or handoff file, and report its current state.

## Output

1. **Waiting on**: what blocks the session. When the user must act, name the exact input. Omit this item when nothing blocks the session.
2. **Goal**: what the session set out to do, in one or two sentences.
3. **Decided**: each choice that shapes the next steps, with its reason. Name a dead end only when it explains a constraint.
4. **Left to do**: the remaining steps, as a list.

## Rules

- At most 25 lines.
- No preamble.
- When the history was compacted and details are missing, name what is missing. Do not guess.
