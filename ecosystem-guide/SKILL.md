---
name: ecosystem-guide
description: "Guide to Scott's agent workflow tools. Use when choosing workflow tooling, validating skills, using recall/search/database tools, or handling secrets safely."
metadata:
  last_updated: "2026-05-14"
  verified_against: "current local skill refresh"
---

# Agent Workflow Ecosystem Guide

A vendor-agnostic map of the tools Scott uses across coding agents. Skills usually activate naturally from the task; use this guide when the user asks which tool fits, how tools relate, or how to combine recall, search, SQLite, MCPs, and secret-safe workflows.

## The Stack

| Tool                 | Type  | Purpose                                                     |
| -------------------- | ----- | ----------------------------------------------------------- |
| **skills**           | Repo  | Canonical portable Agent Skills for compatible harnesses    |
| **check-skills**     | CLI   | Validate/lint portable Agent Skills against agentskills.io  |
| **pirecall**         | CLI   | Sync/search Pi agent sessions in `~/.pi/pirecall.db`        |
| **ccrecall**         | CLI   | Sync/search Claude Code sessions in `~/.claude/ccrecall.db` |
| **nopeek**           | CLI   | Load/use secrets without exposing values to agent context   |
| **mcp-omnisearch**   | MCP   | Unified web/search/AI answers/content extraction            |
| **mcp-sqlite-tools** | MCP   | Safe SQLite inspection, querying, schema work, backups      |
| **mcpick**           | CLI   | Manage MCP servers, plugins, cache, and profiles            |
| **research**         | Skill | Verified source research patterns                           |
| **skill-creator**    | Skill | Create portable Agent Skills with best practices            |

## Decision Tree

**"I need context from previous sessions"**

→ **pirecall** for Pi sessions, **ccrecall** for Claude Code sessions. Use the CLI for quick recall/search, or query the SQLite database directly with **mcp-sqlite-tools** for flexible analysis.

```bash
pnpx pirecall recall "what did we decide about skills?" --json
pnpx pirecall search "mcp-sqlite-tools" --json
pnpx ccrecall recall "last auth work" --json
```

**"I need to search or verify something online"**

→ **mcp-omnisearch** for web search, AI answers, extraction, and source-backed research. Pair with the **research** skill when sources matter.

**"I need to inspect or analyze a SQLite database"**

→ **mcp-sqlite-tools**. Use it for `pirecall.db`, `ccrecall.db`, application SQLite files, CSV-style analysis, schema inspection, backups, and safe read/write separation.

**"I need secrets or .env values available safely"**

→ **nopeek**. Load secret values into the session without printing them into tool output or conversation context.

```bash
pnpx nopeek load .env
pnpx nopeek status
pnpx nopeek audit
```

**"I have too many MCPs eating context"**

→ **mcpick**. Enable only the MCP servers needed for the current project or workflow.

```bash
pnpx mcpick enable omnisearch sqlite-tools
pnpx mcpick disable omnisearch
pnpx mcpick profile save research-mode
```

**"I'm building with Svelte/SvelteKit"**

→ Use the Svelte skills in this repo: `svelte-runes`, `sveltekit-data-flow`, `sveltekit-structure`, `sveltekit-remote-functions`, `svelte-components`, and related skills.

**"I want to create, edit, or validate a skill"**

→ **skill-creator** for new skills; **check-skills** after creating or editing portable Agent Skills; **agent-md-maintenance** for persistent agent instruction files; **ecosystem-guide** when updating the map of tools.

```bash
pnpx check-skills validate ./my-skill
pnpx check-skills validate . --recursive
pnpx check-skills validate . --recursive --no-quality
```

## Typical Workflows

### Skill Authoring + Validation

Use **skill-creator** for authoring guidance, then validate with **check-skills** before finishing.

```bash
pnpx check-skills validate ./my-skill
pnpx check-skills validate . --recursive --llm --quiet
```

Use `--no-quality` when you only want `agentskills.io` spec compliance; omit it for authoring-quality warnings.

### Recall + Database Analysis

```bash
pnpx pirecall sync --json
pnpx pirecall stats --json
```

Then open `~/.pi/pirecall.db` with **mcp-sqlite-tools** for custom SQL across sessions, messages, tool calls, and FTS5 search.

For Claude Code history, use `pnpx ccrecall sync --json` and query `~/.claude/ccrecall.db`.

### Research Mode

Use **mcp-omnisearch** for discovery and extraction, then apply the **research** skill to verify claims and cite sources.

### Data Analysis Mode

Use **mcp-sqlite-tools** for structured data, recall databases, local app databases, or exported datasets.

### Secret-Safe Work Mode

```bash
pnpx nopeek audit
pnpx nopeek load .env
pnpx nopeek status
```

Prefer referencing environment variable names in commands; avoid printing raw values.

### Minimal Context Mode

```bash
pnpx mcpick disable omnisearch sqlite-tools
```

Re-enable only the servers needed for the current task.

## Links

| Tool                | GitHub                                           |
| ------------------- | ------------------------------------------------ |
| skills              | https://github.com/spences10/skills              |
| check-skills        | https://github.com/spences10/check-skills        |
| claude-code-toolkit | https://github.com/spences10/claude-code-toolkit |
| svelte-skills-kit   | https://github.com/spences10/svelte-skills-kit   |
| ccrecall            | https://github.com/spences10/ccrecall            |
| mcp-omnisearch      | https://github.com/spences10/mcp-omnisearch      |
| mcp-sqlite-tools    | https://github.com/spences10/mcp-sqlite-tools    |
| mcpick              | https://github.com/spences10/mcpick              |
