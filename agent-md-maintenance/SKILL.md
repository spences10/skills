---
name: agent-md-maintenance
# prettier-ignore
description: "Maintain agent instruction files effectively. Use when adding lessons learned, updating conventions, or restructuring project instructions."
---

# Agent Instruction File Maintenance

Keep agent instruction files lean, accurate, and useful.

## Quick Start

After mistakes or discoveries, update the instruction file with a reusable rule:

```text
Update the agent instructions so you don't make that mistake again.
```

## When to Update

**Add rules when:**

- Same mistake happens twice
- Non-obvious convention discovered
- Critical project constraint identified

**Remove rules when:**

- Rule no longer applies
- Rule duplicates another rule
- Rule is a one-time fix, not a pattern

## Core Rules

- Keep under 500 lines; extract detail to referenced docs.
- Put commands, conventions, architecture notes, and mistakes to avoid first.
- For Claude Code, global `~/.claude/CLAUDE.md` applies everywhere and project `.claude/CLAUDE.md` applies inside the repo.
- Project-level instructions override global instructions when they conflict.

## References

- [structure-guide.md](references/structure-guide.md) - Section organization
- [lesson-patterns.md](references/lesson-patterns.md) - Writing effective rules
- [hierarchy.md](references/hierarchy.md) - Global vs project scope
