# Next.js + Supabase Kit

This kit configures a coding agent for full-stack TypeScript work with Next.js (App Router) and Supabase (Postgres, Row Level Security, Auth). It favours small, reviewable changes, a database that enforces its own access rules, and a release routine that checks before it ships.

## Working agreement

- Read the existing code before changing it. Follow the patterns already in the repository rather than introducing new ones.
- Make the smallest change that solves the problem. Do not refactor unrelated files in the same change.
- State what you are about to do when the change touches the database schema, auth, or deployment configuration.
- Ask before running destructive commands: dropping tables, resetting a database, deleting migrations, force-pushing, or deploying.
- Never commit secrets. Put values in `.env.local` (git-ignored) and list names only in `.env.example`.
- Report results honestly. If a check did not run or failed, say so; do not claim success.

## Stack conventions

- Use the package manager the repository already uses (check the lockfile). Do not mix managers.
- TypeScript runs in `strict` mode. No `any`, no `@ts-ignore`. Prefer `unknown` plus narrowing, and validate external input with a schema library already in the project (for example zod).
- Server Components are the default. Add `"use client"` only for state, effects, event handlers or browser APIs, and keep the client component as small as possible.
- Fetch data in Server Components or route handlers. Do not fetch in `useEffect` when a server fetch works.
- Server Actions and route handlers must authenticate the caller and validate input on every call. A hidden button is not access control.
- Use `NEXT_PUBLIC_` variables only for values that are safe in browser JavaScript, such as the Supabase URL and publishable (anon) key. The service-role key stays on the server and never reaches a client component.
- Create the Supabase client through the project's helpers (browser, server, middleware). Do not construct ad-hoc clients in components.
- Style with Tailwind utility classes and the project's design tokens. Keep components accessible: semantic elements, labels on inputs, visible focus, keyboard support.

## Database and RLS

- Every table in an exposed schema (normally `public`) gets `alter table ... enable row level security` in the same migration that creates it.
- Write policies per operation (select, insert, update, delete) and per role. Use `(select auth.uid())` so the value is evaluated once per statement.
- Update policies need both `using` and `with check`.
- Index the columns that policies and common queries filter on, especially `user_id` or tenant columns.
- Migrations are forward-only files under `supabase/migrations/`. Never edit a migration that has been applied elsewhere; add a new one.
- Regenerate TypeScript types from the schema after each migration and commit them with the migration.
- Views run with the owner's rights by default; set `security_invoker = true` on views that expose user data.
- Do not add seed or test rows through migrations.

## Auth

- Prefer the server-side session helpers for reading the user. Treat `getUser()` (validated against the auth server) as authoritative; do not trust a session object read from cookies alone for authorisation.
- Redirect targets after sign-in must be same-site paths. Reject absolute URLs.
- Roles and permissions live in the database and are checked by policies, not only in UI code.

## Testing

- Unit-test pure logic (validation, formatting, query builders) with the project's test runner.
- Cover critical user flows (sign-in, create, edit, delete) with Playwright end-to-end tests that use stable locators such as roles and labels, not CSS chains.
- Test RLS with at least two users: one who owns a row and one who does not. The second must be denied.
- A bug fix includes a test that fails without the fix.

## Before you finish

1. Run lint, type-check, tests and a production build using the scripts in `package.json`.
2. Review your own diff: no debug logging, no commented-out code, no unrelated edits.
3. For schema changes, confirm RLS is enabled and policies exist for each operation.
4. Summarise what changed, what you verified, and what you could not verify.

## Skills in this kit

- security-and-hardening: use when handling user input, sessions, secrets or new endpoints.
- auth-implementation-patterns: use when designing sign-in, sessions and role checks.
- postgresql-table-design: use when creating or reviewing tables, types and indexes.
- postgres-database-migration: use when a migration touches existing data.
- sql-optimization-patterns: use when a query or policy is slow.
- e2e-testing-patterns: use when writing or fixing Playwright tests.
- ui-styling: use when building components with Tailwind and shadcn/ui.
- frontend-ui-engineering: use for accessible, responsive pages and forms.
- api-and-interface-design: use when defining route handlers, actions and shared types.
- source-driven-development: use to verify framework APIs against official docs.
- shipping-and-launch: use when preparing a production release.

## Commands

- `new-table`: add a table with migration, RLS, types and tests.
- `rls-audit`: check every table for row level security and sound policies.
- `ship-check`: run all checks and review the diff before release.

## Sub-agents

- `rls-reviewer`: reviews SQL migrations and policies for access control mistakes.
- `nextjs-reviewer`: reviews a diff for server/client boundary, caching and data fetching problems.

## Scoped rules

Agents that support scoped rules load these automatically. If yours does not, read the matching file before editing files it covers:

- `.agents/rules/supabase-rls.md` — for `supabase/**/*.sql`: Applies when editing SQL migrations or Supabase policies.
- `.agents/rules/app-router.md` — for `app/**/*.ts`, `app/**/*.tsx`, `src/app/**/*.ts`, `src/app/**/*.tsx`: Applies when editing App Router pages, layouts, route handlers and server actions.
- `.agents/rules/typescript-strict.md` — always: TypeScript habits that apply to every change in the repository.
