# Setup Guide

How to use this framework with your AI agent tool.

---

## Rules

The six rules in [`rules/`](rules/) are standalone markdown files. Copy them into your agent's configuration directory so they're loaded on every session.

### Cursor

Copy the rule files into `.cursor/rules/` at your project root:

```
.cursor/rules/
├── never-give-up-reading.md
├── never-give-up-planning.md
├── never-give-up-checklist.md
├── never-truncate.md
├── never-trust-agents.md
└── never-trust-syntax.md
```

Cursor loads all `.md` files in this directory as always-on rules.

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

For global rules across all projects, use `~/.claude/skills/` instead.

### Windsurf

Add rule content to your `.windsurfrules` file at the project root. Windsurf reads this as a single file, so concatenate the rules you want:

```
.windsurfrules
```

### Other Tools / Generic

If your AI tool accepts a system prompt or rules file, paste the rule content there. The rules are plain markdown with no tool-specific syntax. They work anywhere the agent reads instructions.

---

## Anti-Pattern Catalog

The [anti-patterns catalog](anti-patterns.md) is a reference document. You don't need to load it into your agent's context. Read it yourself to understand the failure modes, then use the rules (which are the actionable counterpart) in your agent configuration.

If you want the agent to be aware of the anti-pattern names for self-diagnosis, you can include the catalog in your agent's context, but the rules alone are sufficient for behavioral governance.
