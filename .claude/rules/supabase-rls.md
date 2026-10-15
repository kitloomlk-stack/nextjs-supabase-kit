---
paths:
  - "supabase/**/*.sql"
---

# Supabase SQL and RLS

These rules apply to files under `supabase/`.

- Enable row level security in the same migration that creates a table. A table without RLS in an exposed schema is readable and writable by anyone holding the public key.
- Write one policy per operation and role. Name them clearly, for example `profiles_select_own`.
- Use `(select auth.uid())` in policies, not a bare `auth.uid()` call.
- `update` policies need `using` and `with check`. Without `with check`, a user can change a row into one they should not own.
- Add an index on every column a policy filters on.
- Revoke privileges the client roles should not have; grant only the columns users may write.
- Set `security_invoker = true` on views that expose user data.
- Never use the service-role key in code that runs in the browser.
- Prefer new migrations over editing applied ones. Include a matching down migration if the project keeps them.
- Do not insert seed or sample rows in migrations.
