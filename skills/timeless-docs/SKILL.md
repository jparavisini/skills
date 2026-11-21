---
name: timeless-docs
description: >-
  Keeps comments, docs, and agent instructions (CLAUDE.md, AGENTS.md, skills, rules, memory, prompts) true to the current state, with no time-relative words, no change history, and no bans on old values. Use whenever you write or edit a comment, doc, or instruction, above all when you record a correction, and to sweep a repo for stale text. Triggers: "we use X now", "we switched to X", "remember that", "update the docs", "add a comment", "remove old references to X", "sweep the repo for stale notes". Don't use for changelogs, release notes, ADRs, migration guides, commit messages, or PR bodies, where history is the content. For a clarity rewrite, use disambiguate.
---

# timeless-docs

An old value is what a change replaced: a tool, command, endpoint, number, or name.

## Rules

A sentence breaks the rule when it becomes false as time passes:

1. Time-relative words: "now", "currently", "no longer", "recently", "soon", "as of", "new", "old", "still".
2. Change history: what something was, or when or why it changed ("renamed from X", "migrated to Y", "deprecated 2026-03"). Commented-out code is change history.
3. Bans on an old value: "never use gog", "gws, not gog".
4. Promises: "will support", "planned".

"Create a new branch", "if the sync still fails", and a date that is a fact about the system, such as an expiry, pass.

## Fix

1. State the current fact in the present tense: "We use gws now, never use gog" becomes "Gmail: use `gws`."
2. Delete text that holds only history.
3. State a promise as a current limit: "Will support pagination" becomes "Does not paginate."
4. Do not add a ban, because a ban teaches the reader the old value. Keep an existing ban only while the reader can reach the old value: it is installed, on the PATH, or in the code. Strip a kept ban's history: "Never call /v1, it was deprecated in March" becomes "Do not call `/v1`."
5. Report an old value in code, such as a call or an import, and do not change it.

## Record a change

When a fact changes or the user corrects you, search the instruction files, docs, and code comments for the old value. Apply Fix to each hit in place. Do not add a note or a correction entry. When a memory tool cannot edit or delete an entry, tell the user which entry holds the old value.

## Sweep

1. Target: the path the user names, else the git repo root, else the current directory.
2. Ask once for the old values to find; "none" is an answer. When you cannot ask, use the old values that the text marks as replaced.
3. Skip changelogs, release notes, ADRs, migration guides, lockfiles, and vendored code.
4. Search each file for each old value, as a whole word, case-insensitive. Apply Fix to each hit.
5. Read each instruction file in full (CLAUDE.md, AGENTS.md, SKILL.md, rules, memory, prompts). Apply Fix to each sentence that breaks the rule. A full read finds history with no trigger word, such as "gws (not gog)".
6. Search the other docs and code comments for the words in Rules. Apply Fix to each hit that breaks the rule.
7. Outside a git repo, get the user's approval before you write.

Report each file changed with its number of edits, each ban kept, and each old value left in code. When nothing breaks the rule, report "no stale text found".
