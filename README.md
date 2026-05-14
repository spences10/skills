# Agent Skills

Canonical portable Agent Skills for compatible coding agents.

This repo is the source of truth for human-readable skills that can be installed into compatible agent harnesses. Treat skills as high-trust agent instructions: review them before installing and pin versions when possible.

## Use these skills safely

Prefer GitHub CLI `gh skill` on `gh` v2.90.0 or newer.

```bash
# Inspect a skill before installing
gh skill preview spences10/skills svelte-runes

# Install a reviewed skill
gh skill install spences10/skills svelte-runes --agent claude-code

# Safer: pin to a reviewed release tag or commit SHA
gh skill install spences10/skills svelte-runes --agent claude-code --pin <tag-or-commit-sha>

# Check installed skills for updates
gh skill update --dry-run
```

Notes:

- Prefer project-scoped installs for team-shared skills so changes are code-reviewed.
- Review diffs before updating installed skills.
- See [SECURITY.md](SECURITY.md) for the threat model and install guidance.

### Legacy installer

`npx skills add` may still work, but it is no longer the recommended install path here because agent skills are a supply-chain and prompt-injection surface.

If you use it anyway, inspect the repo first and install only reviewed skills:

```bash
# List available skills
npx skills add spences10/skills --list

# Install one reviewed skill
npx skills add spences10/skills --agent pi --skill svelte-runes
```

## Layout

```text
<skill-name>/SKILL.md
```

No harness-specific marketplace files live here. Distribution wrappers sync from this canonical source when they need a curated subset.

## Svelte Skills

- `svelte-code-writer`
- `svelte-core-bestpractices`
- `svelte-components`
- `svelte-deployment`
- `svelte-layerchart`
- `svelte-runes`
- `svelte-styling`
- `svelte-template-directives`
- `sveltekit-data-flow`
- `sveltekit-remote-functions`
- `sveltekit-structure`

## Svelte Skill Refresh Workflow

Before releasing Svelte skill updates:

1. Review the official Svelte AI skills page: <https://svelte.dev/docs/ai/skills>
2. Compare `svelte-code-writer` and `svelte-core-bestpractices` guidance against this repo.
3. Remove legacy Svelte patterns from local examples unless documenting a current compatibility boundary.
4. Update `metadata.last_updated` in changed Svelte `SKILL.md` files.
5. Run `gh skill publish --dry-run` and confirm skills validate before release.

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
