---
name: factory-start
description: Orchestrates one item through the factory declared in `.factory/factory.md`. Each step runs as a fresh agent in its own Herdr pane, and the user approves at every gate from this pane. This pane never does the work. Use when the user says "factory-start <id>", "run the factory on <id>", or "start <id> in the factory". Don't use to run one step yourself; use factory-stage.
compatibility: Needs Herdr (HERDR_ENV=1), the herdr skill, the factory-stage skill, and the agent kinds that `.factory/factory.md` names.
---

# factory-start

Input: an item id. This pane orchestrates and never does a step's work. You may only:

- run herdr commands, with the syntax from the herdr skill
- run the commands in `.factory/factory.md`
- run `git worktree add` and `git worktree remove`
- edit `.factory/factory.md` to demote an agent or to add a decision the user approved
- ask the user with your question tool, such as AskUserQuestion

Never open a file outside `.factory/`, and never read a diff. When you want to fix something, show the problem menu.

## Run the item

1. Stop when `.factory/factory.md` is missing.
2. Read the item. Create a tab labeled `<id>: <title>`, with `--no-focus`.
3. Run the item's step, then each next step. An item at intake starts at triage. Triage runs in the current checkout. Before any later step, create a worktree on branch `factory/<id>` unless it exists, and open every later pane in it.

- **Agent step**: split a new pane in the item's tab. Start the step's agent kind there, named `<step>-<id>` in lowercase. Prompt it: "Use the factory-stage skill: step `<step>`, item `<id>`." Wait until it settles. When it is blocked, show the user what it asks; never answer it. Read its record, the first line of its `factory:` comment.
- **checks**: run every check at once, one pane each. Run a `run:` check as `<command>; echo factory-exit:$?`, wait for `factory-exit:`, and post its record: `done` on exit 0, else `failed`. Run an `agent` check as an agent step. A failed `run:` check, or a `power send-back` agent check that cites a declared rule, sends the item back.
- **Gate**: show the user the records the gate judges. Ask: approve, send back with reasons, or stop. Post the gate's record. On approval, run the gate's `release:` command when it has one.

After a step ends `done` or `approved`, or every check passes, move the item to the next step, or to `released` after the last step. A triage result of `person` ends the run.

On a send-back, pass the reasons in the next prompt. After a gate send-back, search for its reasons, and offer to add a decision when another item has the same reason. On the fourth send-back, show the problem menu instead.

## Problem menu

Show it for an `escalated`, `failed`, or `nothing-to-do` record, a blocked agent, or the fourth send-back:

- **Retry**: a fresh agent, with the user's note in the prompt.
- **Take over**: focus the pane, and wait until the user says done.
- **Send back**, with the user's reasons.
- **Stop**: leave the item at its step.

When an `auto` agent's record is `failed`, set its automation to `confirm`, and tell the user.

## Finish

After the release, close the item's tab and remove its worktree. Report the item's records and any decisions added.
