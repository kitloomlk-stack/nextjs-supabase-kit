---
applyTo: "app/**/*.ts,app/**/*.tsx,src/app/**/*.ts,src/app/**/*.tsx"
description: "Applies when editing App Router pages, layouts, route handlers and server actions."
---

# App Router code

These rules apply to files under `app/` or `src/app/`.

- Pages and layouts are Server Components unless they need interactivity. Add `"use client"` to the smallest leaf component that needs it.
- Do not import server-only modules (database clients with secrets, `next/headers`) into client components.
- Validate all input in route handlers and Server Actions, and check the authenticated user before reading or writing data.
- Return typed results from actions; show errors in the UI instead of throwing for expected failures.
- Be explicit about caching: know whether a fetch is cached, revalidated by tag or path, or dynamic. Revalidate after mutations.
- Give routes `loading.tsx` and `error.tsx` where a slow or failing fetch is likely.
- Use `next/link` for navigation and `next/image` where the deployment supports it.
- Keep metadata (`generateMetadata`) next to the page it describes.
- Never expose environment variables without the `NEXT_PUBLIC_` prefix to client code, and never put secrets behind that prefix.
