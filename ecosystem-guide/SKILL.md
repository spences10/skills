---
name: ecosystem-guide
description: "Guide Scott's LLM tooling ecosystem. Use when choosing recall, search, SQLite, MCP, secret-safety, or skill validation tools."
metadata:
  last_updated: "2026-05-15"
  verified_against: "current local skill refresh"
---

# Agent Workflow Ecosystem Guide

Use this as a router for Scott's agent workflow tools. Keep it vendor-neutral: prefer capabilities first, then mention harness-specific commands only when needed.

## Quick Routing

| Need                                 | Use                                           |
| ------------------------------------ | --------------------------------------------- |
| Previous session context             | `pirecall` for Pi, `ccrecall` for Claude Code |
| Web/docs/source verification         | `mcp-omnisearch` + `research` skill           |
| SQLite inspection or analysis        | `mcp-sqlite-tools`                            |
| Secret-safe `.env` or API key access | `nopeek`                                      |
| Too many MCP servers in context      | `mcpick`                                      |
| Skill creation or validation         | `skill-creator` + `check-skills`              |

## Common Commands

```bash
pnpx pirecall recall "what did we decide?" --json
pnpx ccrecall recall "last auth work" --json
pnpx nopeek load .env --only DATABASE_URL
pnpx check-skills validate . --recursive
pnpx mcpick enable omnisearch sqlite-tools
```

## MCP Setup

Install common MCP tools when a harness supports MCP servers:

```bash
npm i -g mcp-omnisearch mcp-sqlite-tools mcpick
```

- **mcp-omnisearch**: search, AI answers, content extraction
- **mcp-sqlite-tools**: safe SQLite schema/query/write workflows
- **mcpick**: enable/disable MCP servers per task to reduce context noise

## Skill Authoring + Validation

Use `skill-creator` for authoring, then validate before finishing:

```bash
pnpx check-skills validate ./my-skill
pnpx check-skills validate . --recursive --llm --quiet
pnpx check-skills validate . --recursive --no-quality
```
