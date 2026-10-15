---
name: ship-check
description: "Run lint, types, tests and build, then review the diff against a release checklist."
disable-model-invocation: true
---

When invoked:

1. Read `package.json` and run the project's lint, type-check and test scripts, then the production build. Report each result truthfully, including anything that could not run.
2. Review the diff against the base branch. Look for: leftover debug output, commented-out code, unrelated edits, new environment variables missing from `.env.example`, schema changes without RLS, and client components that import server-only code.
3. Check that new migrations are forward-only and that generated types are up to date.
4. List the end-to-end flows affected by this change and whether tests cover them.
5. Produce a short release note and a rollback plan (what to revert, and whether any migration needs a down step).
6. Stop there. Do not deploy, push or tag; hand the checklist to the user.
