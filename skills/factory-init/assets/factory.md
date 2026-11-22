# Factory

A person changes this file. Every agent reads all of it, decisions included, before it acts.

## Source

The item's step is the `factory:<step>` marker in `read` output. An item with no marker is at intake.

- intake: `gh issue list --label factory:intake --json number,title`
- read: `gh issue view {id} --json title,body,labels,comments`
- move: `gh issue edit {id} --remove-label factory:{from} --add-label factory:{to}`
- comment: `gh issue comment {id} --body-file -`
- search: `gh search issues --repo {repo} "{text} in:comments" --json number,title`

## Steps

Steps run in order. A triage result names the next step. A send-back returns the item to the nearest agent step before it.

An agent step names its agent kind and its automation: `confirm` asks before each move, `auto` moves without asking. Gates always ask.

### triage

- agent: claude
- automation: confirm

Read the request. Result `plan` when the design is unsettled. Result `plan-gate` when the request already says exactly what to build. Result `person` when only a person can do it, and say why.

### plan

- agent: claude
- automation: confirm

Write the plan: what changes, the acceptance checks, and the risks. Cite decisions instead of restating them.

### plan-gate

- gate: approve the plan

### build

- agent: claude
- automation: confirm

Implement the approved plan on this worktree's branch. Make its acceptance checks pass. Commit, push, and open a draft pull request.

### checks

- tests: run `npm test`
- review: agent codex, power flag. Review the diff against the plan. Report each finding with its file and line.

### work-gate

- gate: approve the work against the plan and the evidence

### release-gate

- gate: approve the release
- release: `gh pr merge factory/{id} --squash`

## Decisions

One numbered line each. A changed decision is a new line that names the one it replaces.
