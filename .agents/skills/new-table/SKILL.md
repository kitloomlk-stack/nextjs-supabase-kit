---
name: new-table
description: "Add a table with a migration, RLS policies, generated types and a test checklist."
disable-model-invocation: true
---

When invoked with a table name and a short description of its purpose:

1. Read the existing migrations in `supabase/migrations/` and match their naming and style. Ask the user about ownership (per user, per tenant, or shared) if the description does not say.
2. Draft a new migration file that creates the table with sensible types, primary key, `created_at`, foreign keys and constraints.
3. In the same migration, enable row level security and add one policy per operation, using `(select auth.uid())`. Add indexes for the columns the policies filter on.
4. Show the SQL to the user and wait for approval before applying it anywhere.
5. After approval, update the generated TypeScript types using the project's script, and list any code that now needs to change.
6. Propose a short test checklist: owner can read and write, another user cannot, signed-out user cannot.
7. Do not add seed rows.
