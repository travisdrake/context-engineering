# Behavioral Context Engineering

**Everyone engineers what the agent produces. Almost nobody engineers how it operates.**

Context engineering is the discipline of designing the full operating environment for AI agents: not just the information they see, but the behavioral governance that determines whether they produce reliable work or confident-looking mistakes.

This repository extends [Andrej Karpathy's definition](https://x.com/karpathy/status/1936187571242504368) of context engineering into the behavioral layer that most published setups ignore entirely.

---

## The Problem

Most AI agent configurations are rules about **output**: "use TypeScript strict mode," "prefer server components," "follow the repository pattern." These tell the agent what to produce. Nothing tells it how to operate: how to handle uncertainty, when to distrust its own output, how to recover from failures, when to keep going versus stop.

You can give an agent perfect information and it will still cut corners, skip steps, trust its own syntax, and declare victory after partial execution. The information isn't the problem. The behavior is.

## Start Here: The Named Failure Modes

AI agents fail in predictable, nameable ways. The agent doesn't think "I'm cutting corners." It thinks "this is efficient." Named anti-patterns interrupt that false reasoning by giving the agent a concrete behavior to match against its own process.

**[The full anti-pattern catalog](anti-patterns.md)** documents 15 named failure modes, each traced to a specific incident. Here are a few:

**The Trailing Off.** Items 1-5 get detailed implementations with thorough testing. Items 6-7 get shorter treatments. Items 8-9 get a sentence each or are quietly deferred to "follow-up." The quality gradient is the giveaway.

**The Confident Declaration.** Every agent is the coworker with boundless unearned confidence. "I've verified this works" when what it actually did was re-read its own code and decide it looked right. Re-reading your own work is proofreading, not testing.

**The Pass-Through.** A subagent says "no matches found." The main agent tells the user "I couldn't find it." But the subagent searched the wrong directory, used too-narrow search terms, or hit a sandbox restriction. The main agent didn't verify; it passed through the non-result.

Each anti-pattern has a corresponding rule. The rules are in [`rules/`](rules/) and are designed to be copied directly into your agent configuration.

## The Rules

Six standalone behavioral governance rules, each addressing a specific failure mode family:

| Rule | Anti-Pattern It Prevents | Core Mandate |
|---|---|---|
| [never-give-up-reading](rules/never-give-up-reading.md) | The 7% Read | Read every line of a file before planning changes to it |
| [never-give-up-planning](rules/never-give-up-planning.md) | The Trailing Off, The Silent Deferral | If a plan has N items, implement N items |
| [never-give-up-checklist](rules/never-give-up-checklist.md) | The Spot Check, The Category Skip | If a checklist has 50 items, check 50 items |
| [never-truncate](rules/never-truncate.md) | The Courtesy Cut | Never truncate, abbreviate, or omit to save space |
| [never-trust-agents](rules/never-trust-agents.md) | The Pass-Through, The Unchecked Merge | Subagent results are drafts, not facts |
| [never-trust-syntax](rules/never-trust-syntax.md) | The Parse Check, The Confident Declaration | Syntactically correct is not the same as correct |

Each rule is 200-400 words. Total cost: ~1,500 tokens. For behavioral governance, this is extraordinarily cheap insurance.

### Why Not Consolidate?

There's a natural temptation to merge these into a single "quality standards" document. The evidence argues against it:

- Named anti-patterns lose their identity in a list. "The Trailing Off" as the title of its own rule is a mandate. As bullet #3 under "Quality Checks" it's a suggestion.
- Standalone rules are individually testable. You can evaluate whether `never-give-up-planning` is still relevant without reading the other five.
- The agent treats each file as a separate governance constraint. A 200-word focused rule has more behavioral impact than a 2,000-word comprehensive guide.

---

## When Rules Aren't Enough

The first 11 anti-patterns in the catalog are behavioral failures: the agent cuts corners, skips steps, trusts its own output. Behavioral rules fix these because the model has no strong competing prior.

The last 4 anti-patterns are different. They happen when rules fight the model's training distribution: the statistical weight of patterns the model learned during pre-training. You can write "don't use card layouts" and the agent will read it, acknowledge it, and generate cards anyway.

**[Failure-Mode Engineering](pillars/failure-mode-engineering.md)** explains where this boundary is and what to do instead of writing more rules.

## Examples

Working templates for the structural interventions that work when rules don't:

| Example | What It Does |
|---|---|
| [Pre-Commitment Template](examples/pre-commitment-template.md) | Agent states its approach before generating, changing the completion trajectory |
| [Independent Grading Setup](examples/independent-grading-setup.md) | Separate readonly agent grades work, preventing self-confirming scores |
| [Bento Layout Reference](examples/bento-layout.html) | A non-card HTML layout to hand to agents instead of describing what you want |

These aren't rules the agent reads. They're process changes that alter the conditions under which generation happens.

---

## Quick Start

Copy the six rules from [`rules/`](rules/) into your agent's configuration directory. See **[setup.md](setup.md)** for tool-specific instructions (Cursor, Claude Code, Windsurf, and others). Total cost: ~1,500 tokens.

Then write your own. Think about your last AI session. Where did the agent operate badly: not wrong output, but wrong *process*? Did it stop before finishing? Skip verification? Trust its own output without testing?

Name the failure. Write a rule:

```markdown
# Never [Specific Behavior]

## The Rule
[One sentence mandate]

## What This Looks Like
[2-3 specific examples of the anti-pattern]

## What to Do Instead
[2-3 corrective behaviors]

## Why This Exists
Created after [the specific incident that created this rule].
```

A 200-word behavioral rule costs ~150 tokens and prevents hours of wasted work.

For situations where rules aren't enough, see the [examples](examples/) directory.

---

## Principles

1. **Rules from incidents, not theory.** If you can't point to the failure that created the rule, you can't justify the rule. Rules without provenance are opinions.

2. **Named anti-patterns over general advice.** "Don't cut corners" is ignorable. "The Trailing Off: items 1-5 get detailed work, items 8-9 get a sentence each" is matchable.

3. **Behavioral governance over output governance.** The agent's operating discipline matters more than its code style. Most problems aren't "it wrote bad code." They're "it said it was done when it wasn't."

---

## Who This Is For

Anyone running AI agents on real work. The behavioral governance layer applies whether you're building React components, data pipelines, presentations, or internal tools. The failure modes are the same regardless of the task: the agent cuts corners, declares victory early, and trusts its own output without verification.

This framework comes from I/O psychology, where the core discipline is understanding how agents (human ones) behave in structured systems, why they cut corners, and how to design feedback loops that prevent predictable failures. The same frameworks that govern human performance in organizations govern AI agent performance in your IDE.

---

## Acknowledgments

This framework builds on and extends ideas from:

- **Andrej Karpathy**: Coined "context engineering" (June 2025)
- **Rachel Thomas** (fast.ai): "Dark flow" concept
- **Simon Willison**: "Slop" concept; the Lethal Trifecta security model
- **Boris Cherny** (Anthropic): "Once the plan is good, the code is good"

---

## License

[CC BY 4.0](LICENSE.md)

---

*The same patterns that cause humans to cut corners in organizations cause AI agents to cut corners in your IDE. The interventions are the same too: specific, named, and rooted in evidence, not vibes.*
