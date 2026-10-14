# Python Backend & Data Kit

Typed Python services and data work: FastAPI-style backends, pytest, SQL and Postgres design and migrations, data quality checks and tidy notebooks.

A setup for AI coding agents, made by [Kitloom](https://kitloom.site). One source, generated for every major agent: Claude Code, OpenAI Codex, Cursor, Google Antigravity, Gemini CLI, GitHub Copilot, Windsurf (Devin), opencode and Aider.

## Install

1. Download this repository as a ZIP, or use the **Check and download** button on its Kitloom page, which checks it first.
2. Read the files. Nothing here runs on its own: the kit has no hooks and no install scripts.
3. Copy the folders and files you want into the root of your project. `AGENTS.md` is the shared instructions file; edit it to fit your project.

## What is inside

### Skills

- `fastapi-templates` — Starting or restructuring a FastAPI service: routers, dependencies, async patterns.
- `postgresql-table-design` — Designing or reviewing Postgres tables, types, constraints and indexes.
- `postgres-database-migration` — Planning and testing a schema migration against live data.
- `sql-optimization-patterns` — A query is slow; read EXPLAIN output and choose indexes.
- `schema-exploration` — Inspecting an unfamiliar database before writing SQL or answering a data question.
- `data-quality-frameworks` — Adding validation checks and data contracts to a pipeline or dataset.
- `debugging-strategies` — Tracking down a bug or flaky test with a systematic approach.
- `security-and-hardening` — Handling request input, auth, secrets and database access safely.
- `observability-and-instrumentation` — Adding structured logs, metrics and tracing to a service or job.
- `performance-optimization` — Profiling and fixing a measured slowdown in code or queries.

### Commands

Invoke by name (for example `/add-endpoint`).

- `add-endpoint` — Add a typed API endpoint with schemas, tests and error handling.
- `explain-query` — Analyse a SQL query's plan and suggest safe improvements.
- `data-check` — Profile a dataset and propose validation checks before it is used downstream.

### Sub-agents

- `python-reviewer` — Delegate to review a Python diff for typing, error handling, security and test gaps.
- `sql-reviewer` — Delegate to review SQL and migrations for correctness, locking and performance.

### Scoped rules

- `python-typing` — Typing and style habits for every Python change.
- `pytest-tests` — Applies when writing or editing tests.
- `notebooks-sql` — Applies to notebooks and SQL files: keep them reproducible and safe.

## Where each agent finds it

| Agent | Instructions | Skills and commands | Rules | Sub-agents |
|---|---|---|---|---|
| Claude Code | `CLAUDE.md` (imports `AGENTS.md`) | `.claude/skills/` | `.claude/rules/` | `.claude/agents/` |
| OpenAI Codex | `AGENTS.md` | `.agents/skills/` | listed in `AGENTS.md` | `.codex/agents/` |
| Cursor | `AGENTS.md` | `.agents/skills/`, `.claude/skills/` | `.cursor/rules/` | `.claude/agents/` |
| Google Antigravity | `AGENTS.md` | `.agents/skills/` | `.agents/rules/` | `.agents/agents/` |
| Gemini CLI | `AGENTS.md` via `.gemini/settings.json` | `.agents/skills/`, `.gemini/commands/` | listed in `AGENTS.md` | `.gemini/agents/` |
| GitHub Copilot | `AGENTS.md` | `.agents/skills/`, `.github/prompts/` | `.github/instructions/` | `.claude/agents/` |
| Windsurf (Devin) | `AGENTS.md` | `.agents/skills/`, `.windsurf/workflows/` | `.windsurf/rules/` | — |
| opencode | `AGENTS.md` | `.agents/skills/`, `.opencode/commands/` | listed in `AGENTS.md` | `.opencode/agents/` |
| Aider | `AGENTS.md` via `.aider.conf.yml` | — | — | — |

Skills are stored twice (`.agents/skills/` and `.claude/skills/`) because Claude Code reads only its own folder. Agents that read both may list a skill twice; delete the copy you do not need.

## Credits

The skills come from these open-source repositories, each under its own licence. Their licence and a notice are kept beside every copied skill.

| Skill | Source | Licence |
|---|---|---|
| `fastapi-templates` | [wshobson/agents](https://github.com/wshobson/agents) at `46891e7` | MIT |
| `postgresql-table-design` | [wshobson/agents](https://github.com/wshobson/agents) at `46891e7` | MIT |
| `postgres-database-migration` | [timescale/pg-aiguide](https://github.com/timescale/pg-aiguide) at `187be00` | Apache-2.0 |
| `sql-optimization-patterns` | [wshobson/agents](https://github.com/wshobson/agents) at `46891e7` | MIT |
| `schema-exploration` | [timescale/pg-aiguide](https://github.com/timescale/pg-aiguide) at `187be00` | Apache-2.0 |
| `data-quality-frameworks` | [wshobson/agents](https://github.com/wshobson/agents) at `46891e7` | MIT |
| `debugging-strategies` | [wshobson/agents](https://github.com/wshobson/agents) at `46891e7` | MIT |
| `security-and-hardening` | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) at `aeac41d` | MIT |
| `observability-and-instrumentation` | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) at `aeac41d` | MIT |
| `performance-optimization` | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) at `aeac41d` | MIT |

Everything else in this repository (instructions, rules, commands, sub-agents) is by Kitloom under the MIT licence.

## Use at your own risk

Read every file before you use it. Agent instructions can make an agent run commands on your machine. This kit was checked with Kitloom's pre-download check, which looks for warning signs but cannot prove anything is safe.
