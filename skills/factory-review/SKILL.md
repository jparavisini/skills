---
name: factory-review
description: Reports how one agent in the factory declared in `.factory/factory.md` has performed, so the user can decide whether to change its automation. Use when the user says "factory-review <agent>", "can <agent> go auto", or "how is <agent> doing". Don't use to change automation without the user's decision.
---

# factory-review

Input: an agent's step or check name.

1. Run the Source `search` command for `factory: <name> |`.
2. For each item found, run `read`. Take each record of the agent, and the next gate record after it.
3. Report a table: item, outcome, and the gate verdict with its reasons. Then the count of each outcome and of send-backs.
4. Do not recommend a change, and set no threshold. Ask the user whether to change the agent's `automation` or `power`. Edit `.factory/factory.md` only on their answer.
