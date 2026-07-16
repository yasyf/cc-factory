# cc-factory Development Guide

A software factory for Claude Code: orchestrated agents that plan, build, review, and ship software.

## Repository Structure

```
cc-factory/
├── .claude/          # Claude Code settings, guard-hook packs, jj config
├── docs/             # Brand assets (logo, banner, social card)
├── AGENTS.md         # This file — shared conventions
├── STYLEGUIDE.md     # Concrete style rules
├── CLAUDE.md         # Claude-only rules (imports AGENTS.md)
├── CHANGELOG.md      # Keep a Changelog history
└── README.md         # Project overview
```

The factory itself is composed from Claude Code plugin artifacts — skills,
agents, commands, and hooks — that wire together `cc-orchestrate`, `claude-pool`,
`cc-review`, `cc-pushback`, `cc-notes`, and `captain-hook`. Those directories
land here as the pipeline gets built.
