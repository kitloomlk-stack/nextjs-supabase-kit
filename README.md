# Next.js + Supabase Kit

Full-stack TypeScript with Next.js App Router and Supabase: Postgres schema and RLS, auth, Tailwind UI, end-to-end tests and a careful release routine.

A setup for AI coding agents, made by [Kitloom](https://kitloom.site). One source, generated for every major agent: Claude Code, OpenAI Codex, Cursor, Google Antigravity, Gemini CLI, GitHub Copilot, Windsurf (Devin), opencode and Aider.

## Install

1. Download this repository as a ZIP, or use the **Check and download** button on its Kitloom page, which checks it first.
2. Read the files. Nothing here runs on its own: the kit has no hooks and no install scripts.
3. Copy the folders and files you want into the root of your project. `AGENTS.md` is the shared instructions file; edit it to fit your project.

## What is inside

### Skills

- `security-and-hardening` — Handling user input, sessions, secrets or any new endpoint or server action.
- `auth-implementation-patterns` — Designing sign-in, session handling and role checks on top of Supabase Auth.
- `postgresql-table-design` — Creating or reviewing tables, types, constraints and indexes.
- `postgres-database-migration` — Writing a schema migration that will touch existing data.
- `sql-optimization-patterns` — A query is slow or an RLS policy needs an index; read EXPLAIN output.
- `e2e-testing-patterns` — Writing or stabilising Playwright tests for user flows.
- `ui-styling` — Building components with Tailwind and shadcn/ui.
- `frontend-ui-engineering` — Accessible, responsive pages, forms and client state.
- `api-and-interface-design` — Defining route handlers, server action contracts and shared types.
- `source-driven-development` — Checking a Next.js or Supabase API against official docs before using it.
- `shipping-and-launch` — Preparing a production release: checklist, monitoring, rollback plan.

### Commands

Invoke by name (for example `/new-table`).

- `new-table` — Add a table with a migration, RLS policies, generated types and a test checklist.
- `rls-audit` — List every table and check that row level security and policies are correct.
- `ship-check` — Run lint, types, tests and build, then review the diff against a release checklist.

### Sub-agents

- `rls-reviewer` — Delegate to review SQL migrations and policies for access control mistakes.
- `nextjs-reviewer` — Delegate to review a diff for server/client boundary, caching and data fetching problems.

### Scoped rules

- `supabase-rls` — Applies when editing SQL migrations or Supabase policies.
- `app-router` — Applies when editing App Router pages, layouts, route handlers and server actions.
- `typescript-strict` — TypeScript habits that apply to every change in the repository.

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
| `security-and-hardening` | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) at `aeac41d` | MIT |
| `auth-implementation-patterns` | [wshobson/agents](https://github.com/wshobson/agents) at `46891e7` | MIT |
| `postgresql-table-design` | [wshobson/agents](https://github.com/wshobson/agents) at `46891e7` | MIT |
| `postgres-database-migration` | [timescale/pg-aiguide](https://github.com/timescale/pg-aiguide) at `187be00` | Apache-2.0 |
| `sql-optimization-patterns` | [wshobson/agents](https://github.com/wshobson/agents) at `46891e7` | MIT |
| `e2e-testing-patterns` | [wshobson/agents](https://github.com/wshobson/agents) at `46891e7` | MIT |
| `ui-styling` | [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) at `7246805` | MIT |
| `frontend-ui-engineering` | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) at `aeac41d` | MIT |
| `api-and-interface-design` | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) at `aeac41d` | MIT |
| `source-driven-development` | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) at `aeac41d` | MIT |
| `shipping-and-launch` | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) at `aeac41d` | MIT |

Everything else in this repository (instructions, rules, commands, sub-agents) is by Kitloom under the MIT licence.

## Use at your own risk

Read every file before you use it. Agent instructions can make an agent run commands on your machine. This kit was checked with Kitloom's pre-download check, which looks for warning signs but cannot prove anything is safe.
