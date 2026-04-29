# Agent Skills

Canonical portable Agent Skills for compatible coding agents.

This repo is the source of truth for portable skills that can be installed into compatible agent harnesses.

## Install

```bash
# List available skills
npx skills add spences10/skills --list

# Install all skills for a specific agent
npx skills add spences10/skills --agent pi --skill '*'
npx skills add spences10/skills --agent opencode --skill '*'
npx skills add spences10/skills --agent codex --skill '*'

# Install one skill
npx skills add spences10/skills --agent pi --skill svelte-runes
```

## Layout

```text
<skill-name>/SKILL.md
```

No harness-specific marketplace files live here. Distribution wrappers sync from this canonical source when they need a curated subset.

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

## Workflow & Tooling Skills

- `advanced-prompting`
- `analytics`
- `asshole`
- `ci-debug-workflow`
- `agent-md-maintenance`
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

If you want Claude Code plugin marketplaces instead of vendor-agnostic skills:

- [svelte-skills-kit](https://github.com/spences10/svelte-skills-kit) syncs the Svelte skill subset.
- [claude-code-toolkit](https://github.com/spences10/claude-code-toolkit) syncs workflow and tooling skill subsets.

## Sync Reminder

When changing a skill that is distributed by a wrapper repo, run the matching wrapper sync script before releasing the wrapper.

The sync scripts use explicit allowlists, so add new skills there when a wrapper repo should distribute them.
