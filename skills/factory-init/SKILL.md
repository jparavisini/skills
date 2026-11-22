---
name: factory-init
description: Writes `.factory/factory.md`, the one file that declares a factory, where agents do the work, a person approves at gates, and corrections become decisions. Use when the user says "factory init", "make this repo a factory", or "set up a factory". Don't use when `.factory/factory.md` exists; edit it instead.
---

# factory-init

1. Stop when `.factory/factory.md` exists.
2. Copy [assets/factory.md](assets/factory.md) to `.factory/factory.md`.
3. Ask the user which tracker holds the requests. Rewrite the five Source commands for that tracker's CLI. For plain files, use `ls`, `cat`, `mv`, append, and `grep` over `.factory/requests/`.
4. Replace `{repo}` with the repo's name on the tracker. Set the `tests` check to the repo's test command. Leave the other placeholders.
5. Run the `intake` and `search` commands. Fix each command that fails.
6. List what the `move` command needs to exist, such as one label for each step and for `intake`, `person`, and `released`. Create it only after the user approves.
7. Tell the user to commit the file, mark one request with `factory:intake`, and run `factory-start <id>` in a Herdr pane.
