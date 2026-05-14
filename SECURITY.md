# Security

Agent skills are high-trust instructions for AI agents. Installing a skill can change how an agent behaves, and some skill packages may include executable scripts or hidden/prompt-injection instructions.

## This repository

This repository is intended to be a human-readable source collection of portable skills. At the time of writing, it does not ship executable `scripts/` directories or `.sh`, `.py`, `.js`, or `.ts` helper files; the distributed content is primarily Markdown instructions and references, with a small number of non-executable `.svelte` examples.

## Recommended installation

Prefer GitHub CLI `gh skill` on `gh` v2.90.0 or newer:

```bash
# Inspect before installing
gh skill preview spences10/skills svelte-runes

# Install a reviewed skill, preferably pinned to a release tag or commit SHA
gh skill install spences10/skills svelte-runes --agent claude-code --pin <tag-or-commit-sha>
```

Use project scope when sharing skills with a team, and commit the reviewed files so changes are visible in code review.

## Before installing any skill

- Inspect `SKILL.md` and referenced files before use.
- Prefer pinned tags or commit SHAs over floating branches.
- Review diffs before updating installed skills.
- Be cautious with skills containing scripts, network fetches, credential access, shell commands, or instructions like “ignore previous instructions.”
- Treat third-party skills like supply-chain dependencies plus prompt-injection surface.

## Legacy installer

`npx skills add` may still work, but it should be treated as a convenience installer rather than the recommended security posture. Prefer `gh skill` where available because it supports preview, provenance metadata, update checks, and pinning.
