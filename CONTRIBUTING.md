# Contributing

This catalog is curated, not crowdsourced. The bar for inclusion is high by design.

## The Provenance Rule

Every anti-pattern and rule in this repo traces to a specific incident: a real failure, during real work, that cost real time. **If you can't point to the failure, you can't justify the rule.**

This is the single most important principle in the project. It's what separates this catalog from the AI-generated governance files that the ETH Zurich study showed actually make agents worse. Protecting it is non-negotiable.

## What We Accept

**New anti-patterns** that meet all of these criteria:
- Observed in real agent workflows (not hypothetical)
- Reproducible (you've seen it more than once)
- Distinct from the existing 11 named patterns
- Includes the specific incident that surfaced it

**New rules** that meet all of these criteria:
- Addresses a named anti-pattern (existing or proposed with the PR)
- Traces to a specific incident described in the PR
- 200-400 words (consistent with existing rules)
- Follows the four-section structure: The Rule, What This Looks Like, What to Do Instead, Why This Exists

**Setup guide updates** for tools not yet covered or corrections to existing instructions.

**Bug fixes** to existing content (typos, broken links, inaccurate tool instructions).

## What We Don't Accept

- **General best practices** without incident provenance. "Always write tests" is good advice. It's not a behavioral governance rule unless you can describe the specific failure that created it.
- **AI-generated rules.** If an agent wrote it, it doesn't belong here. The whole point is that human-observed, incident-driven rules outperform generated ones.
- **Tool-specific rules.** Rules must be tool-agnostic. They apply to any AI agent, not just Cursor, Claude Code, or any specific IDE.
- **Output governance rules.** "Use TypeScript strict mode" governs output. This repo governs behavior. Different layer.

## How to Submit

1. Open an issue first describing the anti-pattern or rule you want to add, including the incident that created it.
2. Discussion happens in the issue. If the pattern is distinct and well-evidenced, you'll get a green light to PR.
3. PRs without a corresponding issue will be closed.

## Maintenance

When new content is added to the repo (rules, anti-patterns, framework docs, hooks, templates), the PR must also update:
- **setup.md** with installation instructions for the new content across all supported tools
- **README.md** navigation if new sections are added

This keeps the docs current as the repo grows.
