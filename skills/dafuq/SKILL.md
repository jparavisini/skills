---
name: dafuq
description: Rebuilds the agent's last response when it was long, vague, or padded and the user cannot tell what to decide or do. The rebuild leads with the decision, cuts the padding, and stands alone. Use when the user says "dafuq", "wtf", "what?", "huh?", "I'm lost", "wait what", "that made no sense", "say that again but simpler", or sends any short message that shows the last response lost them.
---

# dafuq

The last response failed. The user cannot find what they must decide or do. Rebuild it. Do not defend it, apologize, or resend it with more words.

## Rebuild

1. **Lead with the ask.** The first line, in bold, is the decision the user must make or the action they must take. When nothing waits on the user, the first line is the result.
2. **Rank the options.** For a decision, give 2 to 4 options, the recommendation first, each with a one-line trade-off.
3. **Cut.** The rebuild is at most half the length of the original. No preamble, recap, or closer.
4. **Stand alone.** Define or cut each term that only earlier context explains ("finding 1", a codename). Restate a value where you use it.
5. **Write plain.**
   - Subject, verb, object: "the token's kind controls which records it can write", not "token kind gates record provenance".
   - Literal verbs: controls, holds, shows, allows. Not gates, anchors, surfaces, unlocks.
   - At most 20 words per sentence. Active voice. One instruction per sentence.
   - One term per concept.
   - Steps and conditions in a numbered list. At most 5 items per list.
   - An example in place of an abstract explanation.

## If the user is still lost

Stop rewording. Your model of what they know is wrong. Ask one question to find the gap ("Which part lost you: A, B, or C?"), then answer only that part.
