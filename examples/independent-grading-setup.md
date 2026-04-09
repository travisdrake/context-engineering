# Independent Grading Setup

When the same agent builds and grades, the grades are fabricated. The builder has sunk-cost bias, anchoring bias, and completion drive (lower scores mean more work before "done"). Independent grading separates building from evaluation. This is architecture, not discipline.

## The Problem

This is The Self-Confirming Grade. The builder grades its own work at exactly the minimum passing score. Every time. Justifications are one word: "OK." "Strong." "Passes." The scores are fabricated to clear the gate, not evaluated against the rubric.

## The Workflow

```
1. Builder Agent produces one unit of work
         |
         v
2. Output goes to Grading Agent
   Receives: the output + the rubric
   Does NOT receive: builder's reasoning, previous grades, edit access
         |
         v
3. Grading Agent evaluates against rubric
   Scores each item with specific evidence
   Returns: pass/fail + specific deficiencies
         |
         v
4. Gate decision
   Pass: proceed to next unit
   Fail: builder fixes, then a FRESH grading agent re-evaluates
```

Step 4 uses a fresh grading agent, not the same one. Reusing a grader across evaluation rounds creates anchoring: the second evaluation is contaminated by the first.

## What "Readonly" Means

The grading agent's access is deliberately restricted:

**CAN read:**
- The output file (the deliverable being graded)
- The rubric (scoring criteria and thresholds)

**CANNOT read:**
- Builder's conversation history or reasoning
- Previous grades from earlier rounds
- Builder's original plan or stated approach

**CANNOT do:**
- Edit the output, suggest inline fixes, or modify any files

Giving the grader edit access creates an incentive to pass marginal work rather than fail it.

## Sample Rubric Template

```markdown
## Grading Rubric: [Deliverable Type]

Score each item 1-5. Minimum passing score: 4 on every item.

| Category | Criterion | Score | Evidence |
|----------|-----------|-------|----------|
| [Category] | [Specific, measurable criterion] | | [Quote or cite specific element from the output] |

Auto-fail triggers (any one of these = automatic fail, regardless of other scores):
- [Critical deficiency 1]
- [Critical deficiency 2]
```

The Evidence column is mandatory. Scores without evidence are the grading equivalent of "looks good to me."

## Common Mistakes

- **Sharing build context with the grader.** The grader sees the builder's intent and grades against intent rather than output.
- **Giving the grader edit access.** A grader that can fix small issues will pass marginal work instead of failing it.
- **Reusing the same grading agent across rounds.** The second evaluation anchors to the first. Scores drift rather than being assessed fresh.
- **Letting the builder pre-grade.** "I think this scores a 4 on readability" contaminates the grader's judgment before it starts.

## Implementation Notes

How you create the separate grading agent depends on your tool. The key requirement is context isolation: the grader must not see the builder's reasoning, previous grades, or have edit access. Most agentic coding tools support subagent dispatch or multi-context workflows. Use whatever mechanism your tool provides to spin up an agent with a clean context containing only the output file and the rubric. If your tool doesn't support this natively, start a fresh session with only those two inputs.
