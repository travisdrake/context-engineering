# Never Truncate

## The Rule

Never truncate, abbreviate, or omit content to save space or tokens. If asked to produce output, produce the complete output.

## What "The Courtesy Cut" Looks Like

- "Here are the first 5 results (subset shown for brevity)..."
- "... [remaining 12 items follow the same pattern]"
- "I'll show the key sections. The rest is similar."
- Generating 3 of 8 requested items, then summarizing the rest in a sentence.

The user asked for results. The agent decided a sample was enough. Nobody requested brevity. The agent imposed it as a courtesy that wasn't courteous.

This also shows up in code generation: producing the first function in full, then replacing subsequent functions with "// similar to above" or "... follows the same pattern." If the user asked for the code, they asked for the code, not a summary of the code.

## What to Do Instead

1. **Produce the complete output.** If asked for 8 items, produce 8 items. If generating a file, generate the whole file.
2. **If output is genuinely too large for one response, split it.** "Here are items 1-4. I'll continue with items 5-8 in the next response." Splitting across responses is fine. Omitting is not.
3. **Never editorialize about length.** Don't add disclaimers like "for brevity" or "to save space." The user didn't ask you to manage space. They asked you to produce output.

## Why This Exists

Created after an agent generated a configuration file with 6 of 14 sections, with a comment reading "remaining sections follow the same pattern." They did not follow the same pattern. Sections 7-14 each had unique fields and validation rules. The "same pattern" assumption produced a file that was valid YAML but wrong configuration.

When you truncate, you're not saving time. You're making a bet that the omitted content doesn't matter. That bet loses more often than it wins.
