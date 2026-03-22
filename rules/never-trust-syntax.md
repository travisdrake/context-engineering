# Never Trust Syntax

## The Rule

Syntactically correct is not the same as correct. Verify that changes actually work, not just that they parse.

## What "The Confident Declaration" Looks Like

"I've verified this works" when what the agent actually did was re-read its own code and confirm it looked right. Re-reading your own work is proofreading, not testing. The agent checked that the code was syntactically valid. It didn't check that the code did the right thing.

**The Parse Check** is the sibling pattern. Valid syntax, wrong logic. The linter doesn't complain. The agent declares it done. But the query returns the wrong rows, the function handles the wrong edge case, the component renders in the wrong place.

Variations:

- Writing a database query that parses correctly but joins on the wrong column.
- Creating a configuration file that's valid YAML but specifies the wrong values.
- Building a function that handles the happy path but silently fails on the edge case the user specifically asked about.
- "I've updated the tests" when the tests now pass because they test the wrong thing.

## What to Do Instead

1. **Run the code when possible.** Execute it. Read the output. Not just the exit code: the actual output. Does it produce the expected result?
2. **Test against the requirement, not the implementation.** The question isn't "does this code run?" The question is "does this code do what was asked?" Go back to the original request and verify the output matches.
3. **Check edge cases explicitly.** If the user described a specific scenario, test that scenario. Don't assume the happy path covers it.
4. **If you can't run the code, say so.** "I've written the implementation but was unable to test it in this environment. Here's what should be verified: [specific checks]." Honesty about untested code is better than false confidence about tested code.

## Why This Exists

Created after an agent wrote a data transformation function, confirmed "it works correctly," and delivered it. The function parsed without errors. It also silently dropped every record where a nullable field was null: 40% of the dataset. The agent had verified syntax. It had not verified correctness.

The gap between "it runs" and "it's right" is where the most expensive bugs live.
