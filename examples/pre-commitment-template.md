# Pre-Commitment Template

When an agent starts generating without declaring intent, the first tokens default to the most common patterns in training data. Ask for a dashboard and the agent writes `<div class="card">` before it's even considered an alternative. Pre-commitment changes the starting tokens, which changes the completion trajectory. It's not about making the agent think harder. It's about changing what it writes first.

## The Problem

You ask for a dashboard with an unconventional layout. The agent produces a grid of bordered cards. You say "make it more creative." The agent produces a grid of bordered cards with different colors. Every revision is a variation on the same structure because the underlying token sequence never changed. The first tokens were card tokens, and everything that followed completed the card pattern.

## How It Works

The agent states its approach before generating any output. This changes the initial token sequence. If the agent commits to "I will use a CSS Grid bento layout with asymmetric cells," the first tokens it writes are `<div style="display: grid; grid-template-columns: 2fr 1fr;">` instead of `<div class="card">`. Different starting tokens produce different completions. This is not about discipline or reasoning; it's about initial conditions.

## Template

```markdown
Before generating any [HTML/code/document], state your approach in one sentence:
- What structural pattern will you use? (Name it specifically.)
- What is the first element you will write?

Do not begin generating until you have stated your approach and received confirmation.

If your stated approach produces output that matches common default patterns
(card grids, bordered containers, standard boilerplate), flag this and propose
an alternative before proceeding.
```

Adapt the bracketed term to your domain: HTML, API endpoints, database schemas, test suites.

## Before / After

**Without pre-commitment:**
- Instruction: "Build a dashboard showing three metrics"
- Agent writes: `<div class="card">` (three identical metric cards in a row)

**With pre-commitment:**
- Instruction: "Build a dashboard showing three metrics. State your layout approach first."
- Agent: "I'll use a CSS Grid bento layout with asymmetric cells. The primary metric spans two columns."
- Agent writes: `<div style="display: grid; grid-template-columns: 2fr 1fr;">`
