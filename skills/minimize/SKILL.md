---
name: minimize
description: >-
  Cuts text loaded into an agent's context (a skill, prompt, CLAUDE.md, AGENTS.md, rules file) to the fewest words that still reach its goal. Confirms the goal with the user, sharpens the text with disambiguate, and proves each cut with subagent test runs against the original. Use when the user says "minimize", "simplify this skill", "make this shorter", "cut this down", "trim this prompt", or "how small can this get". Don't use for a rewrite with no length goal; use disambiguate.
---

# minimize

The target is the text to minimize. The goal is what the target makes an agent do.

## 1. Confirm the goal

1. Read the target in full.
2. Write the goal in one sentence, and list 3 to 5 behaviors that show the goal is met.
3. Ask the user to confirm the goal with your question tool, such as AskUserQuestion. Offer your reading first and one or two other readings. Do not continue until the user picks one.

## 2. Write tests

1. Write 3 to 5 test prompts that a real user would type. Each test exercises at least one behavior.
2. Give each test a fixture, such as a small git repo, when the target acts on files.
3. Give each test checks a script can run. Use a pass/fail rubric only for a behavior no script can check.
4. Include the cases most likely to break: edge cases, near misses, and text the target must leave alone.
5. Keep the workspace outside the target's repo.

## 3. Measure the original

1. Record `wc -w` of the target, and copy it to the workspace.
2. Run each test in a fresh subagent with the original, and once with no target.
3. A check that passes with no target marks text the target does not need for that check.
4. Subagents can load the user's own instruction files, so a run with no target is not a bare agent. State this in the report.

## 4. Cut and verify

1. Apply the disambiguate skill to the target.
2. Delete text that only serves checks that pass with no target, and each repeated instruction.
3. Run each test in a fresh subagent with the cut version, each in its own fixture copy. Run a test twice when its result differed between earlier runs.
4. When a check fails, read the output before you blame the target. Fix a wrong check, and rerun every round with the fixed check.
5. When the cut version fails a check that the original passed, restore the fewest words that make the check pass, and rerun.

Repeat step 4 while the cut version passes every check the original passed. Stop when a cut saves less than 5% of the words, or after 3 rounds.

## Report

1. The confirmed goal.
2. Words and pass rate for the original, each round, and no target.
3. What each round cut.
4. Each cut you stopped short of, and the rule or check it would break.
