# Agent Skills

Canonical portable Agent Skills for compatible coding agents.

This repo is the source of truth for skills that are distributed elsewhere through wrapper repos like `svelte-skills-kit` and `claude-code-toolkit`. Each skill lives at the repo root, Matt Pocock-style.

## Install

```bash
# List available skills
npx skills add spences10/skills --list

# Install all skills for a specific agent
npx skills add spences10/skills --agent claude-code --skill '*'
npx skills add spences10/skills --agent pi --skill '*'
npx skills add spences10/skills --agent opencode --skill '*'

# Install one skill
npx skills add spences10/skills --agent claude-code --skill svelte-runes
```

## Layout

```text
<skill-name>/SKILL.md
```

No Claude Code plugin marketplace files live here. Claude-specific distribution is handled by wrapper repos that sync from this canonical source.

## Svelte Skills

- `svelte-components`
- `svelte-deployment`
- `svelte-layerchart`
- `svelte-runes`
- `svelte-styling`
- `svelte-template-directives`
- `sveltekit-data-flow`
- `sveltekit-remote-functions`
- `sveltekit-structure`

## Claude Code Toolkit Skills

- `advanced-prompting`
- `analytics`
- `asshole`
- `ci-debug-workflow`
- `claude-md-maintenance`
- `deslop`
- `ecosystem-guide`
- `improve-codebase-architecture`
- `mcp-setup`
- `nopeek`
- `orchestration`
- `plugin-dev`
- `reflect`
- `research`
- `skill-creator`
- `structured-rpi`
- `tdd`
- `techdebt-finder`
- `terminal-optimization`
- `worktree-mastery`

## Wrapper Repos

- `spences10/svelte-skills-kit` syncs the Svelte skill subset into its Claude Code plugin marketplace.
- `spences10/claude-code-toolkit` syncs toolkit skill subsets into its Claude Code plugin marketplace.

## Sync Reminder

When changing a skill that is distributed by a wrapper repo, run the matching sync script before releasing the wrapper:

```bash
cd ../svelte-skills-kit && ./scripts/sync-from-skills.sh
cd ../claude-code-toolkit && ./scripts/sync-from-skills.sh
```

The sync scripts use explicit allowlists, so add new skills there when a wrapper repo should distribute them.
