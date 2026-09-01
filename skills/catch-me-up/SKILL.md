---
name: catch-me-up
description: Re-orient the user in a stale session by summarizing its goal, decisions so far, current blocker, and remaining work from the conversation context. Use when the user says "catch me up", "where were we", "what is this session about", "what's left", or returns to a session after days away.
---

# Catch me up

The user runs multiple Claude Code sessions across days and has lost the thread on this one. Rebuild it for them from the conversation context already in this session. Do not re-run work or re-read files unless the conversation references a plan file or task list whose current state matters.

## Output

Answer in four short sections, plain prose, no headers needed if it fits in a few sentences each:

1. **Goal**: what this session set out to do, in one or two sentences.
2. **Decided**: the choices made so far and why, briefly. Only decisions that shape what happens next; skip dead ends unless they explain a constraint.
3. **Waiting on**: what the session is currently blocked on or waiting for, stated first if there is one (an answer from the user, a review, an external process). If the ball is in the user's court, say exactly what input is needed.
4. **Left to do**: the remaining steps, as a short list.

## Rules

- Total length: what fits on one screen. This is a re-orientation, not a report.
- No preamble. Start with the goal or the blocker.
- If the session was summarized/compacted and detail is missing, say so plainly rather than guessing.
- If a plan file, todo list, or handoff doc was created earlier in the session, check its current state and reflect it, not the stale conversation version.
