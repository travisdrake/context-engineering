# Never Trust Agents

## The Rule

Subagent results are drafts, not facts. Verify before passing them to the user.

## What "The Pass-Through" Looks Like

A subagent says "no matches found." The main agent tells the user "I couldn't find it." But the subagent searched the wrong directory, used too-narrow search terms, or hit a sandbox restriction. The main agent didn't verify; it passed through the non-result as if it were authoritative.

Variations:

- A subagent reports "all tests pass" but only ran 3 of 12 test files.
- A subagent summarizes a document but misses a critical section. The main agent passes the summary to the user as complete.
- Two subagents return results about different parts of a system. The main agent merges them without checking for contradictions. The merged summary contains conflicting claims that neither subagent would have produced alone.

The pattern: the main agent treats delegation as absolution. "I asked someone to check. They said it's fine. Therefore it's fine." But delegating work doesn't mean delegating responsibility.

## What to Do Instead

1. **Verify key claims.** When a subagent reports a finding (or a non-finding), do a quick independent check. Search the directory yourself. Read the file yourself. Confirm the result isn't an artifact of a too-narrow search or a sandbox limitation.
2. **Check for completeness.** Did the subagent cover the full scope of the request, or just part of it? "No matches" might mean "no matches in the one directory I checked."
3. **Cross-check merged results.** If combining output from multiple subagents, verify consistency. Do the results agree on shared facts? Do the scopes cover the full request without gaps?
4. **Report uncertainty.** If you can't fully verify a subagent's result, tell the user: "A subagent reported X. I was able to confirm Y but couldn't independently verify Z."

## Why This Exists

Created after a subagent searched for a function definition in the wrong subdirectory and returned "not found." The main agent told the user the function didn't exist. It did exist, 40 lines into a file the subagent never opened. The user spent an hour recreating a function that was already written.

Trust is earned by verification, not by delegation.
