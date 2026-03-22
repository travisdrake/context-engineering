# Named Anti-Patterns: The Failure Mode Catalog

Every rule in this framework traces to a specific failure. These aren't hypothetical risks. They're named, documented behaviors that AI agents exhibit predictably and repeatedly.

The agent doesn't think "I'm cutting corners." It thinks "this is efficient." Named anti-patterns interrupt that false reasoning by giving the agent a concrete behavior to match against its own process.

---

## The Catalog

### The Spot Check

Running 5 of 50 checklist items and declaring the check complete. The items you skip are the ones most likely to have issues: the agent avoids the items it's least confident about.

**Rule:** [never-give-up-checklist](rules/never-give-up-checklist.md)

### The Trailing Off

Items 1-5 get detailed implementations with thorough testing. Items 6-7 get shorter treatments. Items 8-9 get a sentence each or are quietly deferred to "follow-up." The quality gradient is the giveaway.

**Rule:** [never-give-up-planning](rules/never-give-up-planning.md)

### The Silent Deferral

"The remaining items are straightforward and can be done in a follow-up session." The user didn't ask to defer them. The agent decided to stop.

**Rule:** [never-give-up-planning](rules/never-give-up-planning.md)

### The Courtesy Cut

"Here are the first 5 results (subset for brevity)..." The user asked for results, not a sample. The agent decided 5 was enough without being asked.

**Rule:** [never-truncate](rules/never-truncate.md)

### The Pass-Through

A subagent says "no matches found." The main agent tells the user "I couldn't find it." But the subagent may have searched the wrong directory, used too-narrow search terms, or hit a sandbox restriction. The main agent didn't verify; it passed through the non-result.

**Rule:** [never-trust-agents](rules/never-trust-agents.md)

### The Confident Declaration

"I've verified this works" when what the agent actually did was re-read its own code and confirm it looked right. Re-reading your own work is proofreading, not testing.

**Rule:** [never-trust-syntax](rules/never-trust-syntax.md)

### The Parse Check

Valid syntax, wrong logic. The linter doesn't complain. The agent declares it done. But the query returns the wrong rows, the function handles the wrong edge case, the component renders in the wrong place.

**Rule:** [never-trust-syntax](rules/never-trust-syntax.md)

### The Unchecked Merge

Two subagents return results about different parts of the codebase. The main agent merges them into a summary without verifying they're consistent or complete. Contradictions pass through undetected.

**Rule:** [never-trust-agents](rules/never-trust-agents.md)

### The Vague Completion

Marking a task as "completed" after a partial implementation. The checkbox says done; the file says otherwise.

**Rule:** [never-trust-syntax](rules/never-trust-syntax.md)

### The Category Skip

Checking "Structure" and "Visual Design" sections of a checklist but skipping "Interaction Diversity" and "Content Communication." Every category exists because something went wrong without it.

**Rule:** [never-give-up-checklist](rules/never-give-up-checklist.md)

### The 7% Read

The agent reads the first 30 lines of a 400-line file, decides it understands the structure, and plans changes based on what it assumes the rest contains. It saw 7% of the file. It planned with 100% confidence.

**Rule:** [never-give-up-reading](rules/never-give-up-reading.md)

---

## Why Naming Works

Three reasons:

1. **Pattern matching.** The agent can compare its current behavior against a named list. "Am I about to do The Trailing Off?" is a concrete question. "Am I being thorough?" is not.

2. **Psychological weight.** A rule named `never-give-up-planning` that exists as its own file feels like a mandate. Section 3 of a "quality standards" doc feels like item #3 on a list. Standalone rules with failure-mode names carry more compliance weight than consolidated guidelines.

3. **Provenance.** Each named anti-pattern traces to a real incident. The provenance makes the rule feel earned, not arbitrary. Rules without provenance are opinions; rules with provenance are governance.

---

## Building Your Own Catalog

Think about your last AI session. Where did the agent operate badly: not wrong output, but wrong *process*?

- Did it stop before finishing?
- Did it declare something done when it wasn't?
- Did it skip a verification step?
- Did it trust its own output without testing?
- Did it compress or truncate without being asked?

Name the failure. Write a rule. A 200-word behavioral rule costs roughly 150 tokens and prevents hours of wasted work.

See the [rule template](rules/) and the six rules in this repo for the pattern to follow.

---

*Each anti-pattern is a prediction. Each rule is insurance. The catalog grows as you encounter new failure modes, and every addition makes the system more reliable. This is the aviation safety model: the rules didn't come from theory. They came from crashes.*
