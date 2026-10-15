# TypeScript habits

- Keep `strict` on. Do not weaken `tsconfig.json` to make an error disappear.
- No `any` and no `@ts-ignore`. If a type is truly unknown, use `unknown` and narrow it. If a suppression is unavoidable, use `@ts-expect-error` with a reason.
- Derive types from the source of truth: generated Supabase types for rows, schema inference for validated input.
- Validate data that crosses a trust boundary (request bodies, query strings, webhook payloads, JSON columns) before using it.
- Prefer named exports, small modules and explicit return types on exported functions.
- Handle `null` and `undefined` from queries; a `maybeSingle()` result may be empty.
- Do not leave `console.log` in committed code.
- Match the formatting and lint rules already configured; do not reformat files you are not changing.
