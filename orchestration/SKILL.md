---
name: orchestration
# prettier-ignore
description: "Coordinate parallel agent work. Use when decomposing complex tasks, running review/implementation in parallel, managing task lists, or isolating work with branches/worktrees."
metadata:
  last_updated: "2026-05-15"
  verified_against: "current local skill refresh"
---

# Orchestration

Coordinate multi-agent or multi-session coding work without file conflicts or duplicated effort. Stay harness-agnostic: use built-in team/subagent features when available, or manual git worktrees when not.

## When to Use

- Complex work that can split by domain, file area, or risk level
- Parallel review, implementation, test, or documentation passes
- Background research while the main session implements
- Risky changes that should be isolated in branches or worktrees

## Core Rules

- Assign clear ownership: one agent/session owns each file or subsystem.
- Prefer 3-5 parallel workers; more usually adds coordination overhead.
- Create a shared task list with dependencies and acceptance criteria.
- Require concise handoff notes: files touched, decisions made, validation run, blockers.
- Synthesize results in the lead session before merging or committing.

## Worktree Pattern

Use git worktrees when parallel sessions may mutate files:

```bash
git worktree add ../project-review main
git worktree add ../project-refactor main
git worktree list
```

Each session works in its own directory, then syncs through commits, branches, or patches.

## Decomposition Patterns

| Pattern              | Use when                                |
| -------------------- | --------------------------------------- |
| Fan-out              | Same operation across independent areas |
| Pipeline             | Research → implement → test → docs      |
| Reviewer/implementer | One session changes, another critiques  |
| Speculative branches | Trying competing approaches safely      |
| Background monitor   | Long-running CI, logs, or investigation |

## References

- [patterns.md](references/patterns.md) - Orchestration patterns
- [domains.md](references/domains.md) - Domain-specific decomposition
- [task-management.md](references/task-management.md) - Dependencies, task graphs, file partitioning
- [worktree-commands.md](references/worktree-commands.md) - Git worktree command reference
- [session-strategies.md](references/session-strategies.md) - Multi-session patterns
- [cleanup.md](references/cleanup.md) - Worktree removal and maintenance
