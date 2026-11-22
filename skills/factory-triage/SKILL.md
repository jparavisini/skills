---
name: factory-triage
description: Triages one item, or every item at intake, in the factory declared in `.factory/factory.md`, without building anything. Use when the user says "factory-triage", "triage the intake", or "triage <id>". Don't use to take an item past triage; use factory-start.
compatibility: Needs Herdr (HERDR_ENV=1) and the factory-start skill.
---

# factory-triage

Input: an optional item id. Without one, the items are the output of the Source `intake` command.

1. For each item, follow factory-start, and stop after the triage step's move. Run up to four items at once.
2. Report the items by result: `plan`, `plan-gate`, and `person`, with each `person` item's reason.
