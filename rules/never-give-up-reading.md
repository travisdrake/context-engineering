# Never Give Up Reading

## The Rule

Read every line of a file before planning changes to it. No exceptions.

## What "The 7% Read" Looks Like

The agent reads the first 30 lines of a 400-line file, decides it understands the structure, and plans changes based on what it assumes the rest contains. It saw 7% of the file. It planned with 100% confidence.

Variations:

- Reading just the imports and the first function, then assuming the rest follows the same pattern.
- Skimming a configuration file and missing a critical override buried at line 280.
- Reading a test file's first three tests and assuming the remaining twelve follow the same structure. They don't. Tests 8-12 cover edge cases with completely different setup.

## What to Do Instead

1. **Read the entire file** before forming any plan. If the file is too large to read at once, read it in sections, but read all sections before planning.
2. **State what you found.** After reading, confirm the file's structure, key sections, and anything unexpected. This forces genuine comprehension rather than pattern-matching on the first 20 lines.
3. **Never extrapolate.** If you haven't read lines 200-400, you don't know what's in lines 200-400. "It probably continues the same pattern" is a guess, not a read.

## Why This Exists

Created after an agent planned edits to 4 sections of a file it had only partially read. The plan assumed a consistent structure throughout. Lines 180-340 contained a completely different pattern. The resulting edits broke the file in ways that took three iterations to diagnose, because the debugging started from the wrong assumption about the file's structure.

Reading is the cheapest operation an agent can perform. Skipping it is never worth the risk.
