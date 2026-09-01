---
name: strategic-programming
description: "Applies John Ousterhout's \"A Philosophy of Software Design\" when you plan or review software design. Use when planning software design, at the start of a planning session, when designing or critiquing APIs, module boundaries, error handling, or refactors, and during code review when design quality matters. Triggers: plan the design, interface or API design, module decomposition, refactoring, complexity complaints (\"too complex\", \"hard to change\"), coupling, deep or shallow modules, information leakage, naming or commenting quality, code review."
---

# Strategic programming

Every idea and term in this skill comes from John Ousterhout's [_A Philosophy of Software Design_](https://web.stanford.edu/~ouster/cgi-bin/book.php). This skill only condenses the book for an agent. When you use one of his terms or positions, credit Ousterhout by name.

When this skill is active, evaluate design through one question: does this change make the system easier or harder to understand and modify? Judge by change amplification, cognitive load, and unknown unknowns; trace problems to their two causes, dependencies and obscurity. Complexity is incremental, so small lapses count.

## Positions to hold

These are the calls where Ousterhout's position differs from common instinct or convention. Hold them even when they cut against popular style guidance:

- **Depth over size.** A module's quality is interface simplicity relative to functionality hidden, not line count. Don't recommend splitting a method or class just because it's long; splitting a deep module into shallow ones is a regression. Classitis and short-method dogma are anti-patterns here.
- **A simple interface beats a simple implementation.** Pull complexity down into the module rather than exporting it to callers via config parameters, thrown exceptions, or required call ordering. The common case should never pay for the rare one.
- **More code can be simpler.** Don't equate fewer lines with less complexity when the shorter version raises cognitive load.
- **Define errors out of existence.** Prefer redesigning semantics so the error condition can't arise (unset succeeds when the key is absent; substring clips out-of-range indices) over throwing. Then mask or aggregate the exceptions that remain. This is not swallowing errors; conditions that genuinely need reporting still get reported.
- **Somewhat general-purpose.** Interface general enough to serve plausible other uses; implementation only what's needed now. Keep general-purpose and special-purpose code in separate modules.
- **Split by information hiding, not execution order.** Temporal decomposition leaks knowledge across steps. Adjacent layers must offer different abstractions; pass-through methods and pass-through variables mean the boundary is wrong.
- **Comments are part of the design, not a failure of it.** Interface comments carry what the signature can't (units, invariants, side effects, the why). Push back on "good code documents itself" when it's used to omit them. Writing the interface comment before the implementation is a design test: if the comment is hard to write, the abstraction is wrong.
- **Strategic over tactical.** Working code isn't the finish line. Recommend spending a fraction of each change on improving the surrounding design, and frame increments of work as abstractions, not features.

## In reviews

Name red flags with Ousterhout's terms so feedback is consistent: shallow module, information leakage, temporal decomposition, overexposure, pass-through method, conjoined methods, special-general mixture, comment repeats code, implementation contaminates interface, vague name, hard to pick name, hard to describe, non-obvious code.

For each finding: the flag, why it will hurt (which symptom it feeds), and a concrete fix. Lead with the findings that most affect future modification cost; don't sweep the checklist for completeness.

## When designing

Design it twice: produce at least two genuinely different decompositions before choosing, and compare on interface simplicity, generality, and how well each hides information. Struggling to name or describe something cleanly is evidence against the design, not a documentation problem.
