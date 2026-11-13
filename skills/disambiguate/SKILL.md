---
name: disambiguate
description: >-
  Rewrites text loaded into an LLM's context (a skill, CLAUDE.md, AGENTS.md,
  a rules or memory file, a prompt, a spec, a doc) so each sentence is necessary,
  singular, unambiguous, and verifiable, with one term per concept. Returns
  the rewritten text with fewer words, a glossary of the terms it fixed, and
  questions only where the text is ambiguous or underspecified. Use when
  writing or reviewing anything loaded into an LLM's context.
compatibility: >-
  Needs wc. No network. In a non-interactive run it cannot ask questions,
  so it reports them and leaves those passages unchanged.
metadata:
  version: "1.4"
---

# disambiguate

Apply the requirement-quality characteristics of ISO/IEC/IEEE 29148 to text loaded into an LLM's context.

## Inputs

- The text: one or more files, or text passed in the conversation. Write conversation text to a scratch file first. With no text given, ask once.
- The files that set the terms already in use: the repo's `CLAUDE.md` or `AGENTS.md`, and the files the target links to.

## Process

1. **Measure.** Record `wc -w` for each file.
2. **Read the whole text** before you rewrite any of it. List the concepts it names and the term it uses for each.
3. **Necessary.** Delete each sentence whose removal would not change what the LLM does: general knowledge, restatements, motivation, preambles, summaries, and change history.
4. **Singular.** Split each sentence that gives two instructions.
5. **Unambiguous.** Give each concept one term, and replace its synonyms everywhere except inside a passage that step 7 makes a question; that passage stays verbatim until its question is answered. When a published source defines a term for the concept, use that term and cite the source; otherwise keep the text's term. Choose a term with one meaning in the text's domain; when a term has several common senses, use a narrower term. Replace each vague pronoun ("this", "it", "that") with its noun.
6. **Verifiable.** Find the words that set no testable condition: subjective words ("appropriate", "properly", "clean", "relevant"), loopholes ("if possible", "as needed", "try to", "ideally", "usually"), open endings ("etc.", "and so on"), and comparatives with no baseline ("better", "simpler"). Replace each with a threshold, an example, or a check. Delete every intensifier ("very", "carefully", "really") and every capitalized emphasis word ("IMPORTANT", "MUST").
7. **Sort what remains.** When the surrounding text or a linked file states which reading is meant, rewrite to that reading. Make a question of each passage that is ambiguous (two readings conflict), underspecified (a fact is missing), or whose rule contradicts the published meaning of its own term. Never pick a reading in silence.
8. **Ask.** Ask all questions in one batch. Each question quotes the passage, names the readings, and puts the recommended reading first. In a non-interactive run, skip this step and leave the questioned passages unchanged.
9. **Write.** Rewrite the files in place, or return conversation text in a fenced block. A rewrite changes what the LLM does only through an answered question.
10. **Check.** Record `wc -w` again for each rewritten file. When the count is not lower and no answer added a fact, run steps 3 to 6 once more. Then stop, and report a count that is still not lower with the steps that added words.

## Output

Per file:

- Words before and after, or "no change" for a file that needed no rewrite.
- The glossary: each term you fixed, its one-line definition, and its source, or "no standard term".
- The questions and the answers applied, or the open questions in a non-interactive run.

Done when every file is rewritten or reported as "no change", and every question is answered or reported.
