---
name: dafuq
description: The user is confused by your last response and needs it reworded. Trigger on "dafuq", "/dafuq", "wtf", "what?", "huh?", "I'm lost", "wait what", "that made no sense", "say that again but simpler", or any short message signaling the previous reply confused them.
---

# dafuq

The last response failed. Do not defend it, apologize at length, or resend it with more words. Rebuild it.

## Rules

1. **Start over from the one central point.** State the single most important thing in one plain sentence. If you can't state it in one sentence, find the point before rewriting.
2. **Shorter, not longer.** The reword must be at most half the length of the original. More words make the reword harder to follow.
3. **No orphaned references.** Any term whose meaning lives only in earlier context ("finding 1", "the spine", a codename) gets defined on first use or cut. The reword must stand alone.
4. **No AI dialect.** Unpack noun stacks ("token kind gates record provenance") into subject-verb-object sentences ("the token's kind controls which records it can write"). Replace metaphor verbs (gates, anchors, surfaces, unlocks) with literal ones (controls, holds, shows, allows). If a phrase would never be said out loud to a colleague, rewrite it.
5. **Sentence discipline**:
   - Max 20 words per sentence for instructions, 25 for descriptions.
   - Active voice, simple tenses. "The server rejects X", not "X will have been rejected".
   - One instruction per sentence. One topic per paragraph, max 6 sentences.
   - Use one word for one meaning throughout the message. Don't alternate "record/entry/row" for the same thing.
   - Sequences and conditions go in numbered lists, not prose.
6. **Concrete over abstract.** If the original explained a concept, the reword shows an example. If it gave options, name one recommendation and one reason.
7. **End with one check.** Finish with a single question that tests whether it landed, aimed at the likeliest sticking point ("Does the part about X make sense, or is that where it broke?"). Not "does that help?".

## If it happens twice

The problem is your model of what they know, not your wording. Stop rewording. Ask one question to find the actual gap ("Which part lost you: A, B, or C?"), then answer only that part.
