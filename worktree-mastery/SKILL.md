---
name: worktree-mastery
# prettier-ignore
description: "Git worktree patterns for parallel agent sessions. Use when running multiple coding-agent instances on the same repo, isolating risky work, or avoiding branch/stash conflicts."
---

# Worktree Mastery

Run 3-5 parallel agent sessions on the same repo. "The single biggest productivity unlock." - Boris Cherny

## Core Concept

Git worktrees = independent working directories sharing one repo. Each agent session gets its own worktree. No branch conflicts, no stash juggling.

## Quick Setup

```bash
# From repo root, create worktrees
git worktree add ../myproject-review main
git worktree add ../myproject-refactor main
git worktree add ../myproject-test main

# List active worktrees
git worktree list
```

## Naming Convention

```
myproject/           # Main worktree (original clone)
myproject-review/    # Code review session
myproject-refactor/  # Refactoring session
myproject-test/      # Test writing session
myproject-docs/      # Documentation session
```

## Session Strategy

| Worktree      | Use Case                     |
| ------------- | ---------------------------- |
| main          | Primary development, commits |
| main-review   | PR reviews, code reading     |
| main-refactor | Large refactors, experiments |
| main-test     | Test writing, debugging      |

## Workflow

1. **Create worktrees** before starting parallel work
2. **Start your coding agent** in each worktree directory
3. **Work independently** - each session has isolated state
4. **Sync via git** - commit in one, pull in another
5. **Cleanup** when done

## Sync Between Sessions

```bash
# In worktree needing updates
git fetch origin
git rebase origin/main

# Or if working on branches
git checkout feature-branch
git pull
```

## References

- [worktree-commands.md](references/worktree-commands.md) - Full command reference
- [session-strategies.md](references/session-strategies.md) - Multi-session patterns
- [cleanup.md](references/cleanup.md) - Removal and maintenance
