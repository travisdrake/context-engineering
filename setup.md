# Setup Guide

How to use this framework with your AI agent tool.

---

## Rules

The six rules in [`rules/`](rules/) are standalone markdown files. Copy them into your agent's configuration directory so they're loaded on every session.

### Cursor

Copy the rule files into `.cursor/rules/` at your project root, renaming them to `.mdc` and adding frontmatter:

```
.cursor/rules/
├── never-give-up-reading.mdc
├── never-give-up-planning.mdc
├── never-give-up-checklist.mdc
├── never-truncate.mdc
├── never-trust-agents.mdc
└── never-trust-syntax.mdc
```

Each `.mdc` file needs frontmatter to be always-on:

```yaml
---
description: "Behavioral governance rule: [rule name]"
globs: []
alwaysApply: true
---

[paste rule content here]
```

Cursor uses `.mdc` files with frontmatter for its rules system. Plain `.md` files in this directory won't get the always-on behavior.

### Claude Code

Add the rule files to your project's `.claude/skills/` directory as always-on skills, or paste the rule content directly into your `CLAUDE.md` at the project root. Claude Code reads both at session start.

```
.claude/skills/
├── never-give-up-reading.md
├── never-give-up-planning.md
├── never-give-up-checklist.md
├── never-truncate.md
├── never-trust-agents.md
└── never-trust-syntax.md
```

For global rules across all projects, use `~/.claude/skills/` instead. Project-level is safer if you want to scope rules per-repo.

### Windsurf

Add rule content to your `.windsurfrules` file at the project root. Windsurf reads this as a single file, so concatenate the rules you want:

```
.windsurfrules
```

### Other Tools / Generic

If your AI tool accepts a system prompt or rules file, paste the rule content there. The rules are plain markdown with no tool-specific syntax. They work anywhere the agent reads instructions.

---

## Verify It's Working

After setup, give your agent a task with 5+ steps and watch for explicit item tracking ("Implementing item 3 of 7"). If the agent acknowledges the count and works through each item, the planning rule is active. If it silently skips items or trails off at the end, the rules aren't loading.

A faster test: ask the agent to read a long file and summarize it. If it reads the whole file before responding (rather than skimming the first section), the reading rule is active.

### Which Rules to Start With

All six rules cost ~1,500 tokens total. There's no reason not to use all of them. But if you want to start small and see immediate impact:

1. **never-give-up-planning** (The Trailing Off): most common failure, most visible improvement
2. **never-trust-syntax** (The Confident Declaration): catches the "I've verified this works" lie
3. **never-truncate** (The Courtesy Cut): stops silent omissions in results

Add the other three when you're ready. They're all standalone.

---

## Anti-Pattern Catalog

The [anti-patterns catalog](anti-patterns.md) is a reference document. You don't need to load it into your agent's context. Read it yourself to understand the failure modes, then use the rules (which are the actionable counterpart) in your agent configuration.

If you want the agent to be aware of the anti-pattern names for self-diagnosis, you can include the catalog in your agent's context, but the rules alone are sufficient for behavioral governance.

---

## Pillar Docs

Pillar docs (in `pillars/`) are reference material explaining the concepts behind the rules. They are not loaded into agent context. Read them yourself to understand when rules work and when you need structural interventions instead.

## Examples

Examples (in `examples/`) are working templates and reference files:

- **Process templates** (`pre-commitment-template.md`, `independent-grading-setup.md`): Adapt these into your workflow. They describe process changes, not agent rules.
- **Reference layouts** (`bento-layout.html`): Hand these directly to your agent when you need non-default output. Include the file content in your prompt or point the agent to the file path. Concrete examples produce better results than prose descriptions.
