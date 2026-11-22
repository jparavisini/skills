---
name: factory-stage
description: Runs one step of a factory declared in `.factory/factory.md` on one item, and records the result on the item. Use when told to run a factory step, agent, or check on an item, or when a person takes over a step. Don't use to move an item between steps or to approve at a gate; factory-start does that.
---

# factory-stage

Inputs: a step name and an item id.

1. Read `.factory/factory.md` in full, and find the step's brief.
2. Read the item. Its records hold the plan, the findings, and the reasons for each send-back.
3. Do the brief's work in the current directory. Follow every decision.
4. Post one record with the Source `comment` command. Its first line is `factory: <step> | <outcome>`, plus `| <result>` when the brief names results. The body holds what the next reader needs, such as the plan or the findings.

The outcome is `done`, `escalated` (a person must decide something; say what), `nothing-to-do`, or `failed` (say why).

Never move the item, release it, or approve it.
