---
name: "rls-audit"
description: "List every table and check that row level security and policies are correct."
---

When invoked:

1. Read the migrations under `supabase/migrations/` (and `supabase/schemas/` if present) and build a list of every table in exposed schemas.
2. For each table report: whether RLS is enabled, which policies exist per operation, which roles they target, and whether each policy has an index on the columns it filters.
3. Flag these problems: RLS disabled; no policy for an operation that the app uses; `update` without `with check`; policies that use `true` or only check that a user is authenticated when ownership is intended; views without `security_invoker`; grants to `anon` that look unintended.
4. Search the application code for the service-role key and for client-side uses of it, and report any.
5. Output a table of findings ordered by severity, each with the file and a suggested fix. Do not modify files unless the user asks.
