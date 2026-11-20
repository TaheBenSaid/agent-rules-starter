# Fieldnote

## Project

Web app where small teams write and share field reports. Next.js 15 with the App Router,
TypeScript, Tailwind, Postgres through Drizzle. Deployed as a single Node server.
Package manager is pnpm.

## Commands

- Install: `pnpm install`
- Dev server: `pnpm dev` (http://localhost:3000)
- Test: `pnpm test` (Vitest)
- Test one file: `pnpm test src/lib/reports.test.ts`
- End to end: `pnpm exec playwright test`
- Lint: `pnpm lint`
- Type check: `pnpm exec tsc --noEmit`
- Build: `pnpm build`
- New migration: `pnpm exec drizzle-kit generate`

## Architecture

- `src/app/`: routes. Each folder is a URL segment with `page.tsx`, `layout.tsx`, `loading.tsx`.
- `src/app/api/`: route handlers, only for webhooks and third parties.
- `src/components/ui/`: shared primitives. Check here before building a new one.
- `src/lib/db/`: Drizzle schema and queries. Only server code imports from here.
- `src/lib/actions/`: server actions for mutations.
- `drizzle/`: generated migrations. Don't edit by hand.

## Rules

Do:

- Keep components as server components. Add `"use client"` only for state, effects or browser APIs.
- Fetch data in server components or server actions, not in `useEffect`.
- Validate every server action input with the zod schema next to it.
- Use `next/image` for images and `next/link` for internal links.
- Read env vars through `src/lib/env.ts`, never `process.env` directly.

Don't:

- Import `src/lib/db` from a file with `"use client"`.
- Use the Pages Router or `getServerSideProps`.
- Add a dependency without asking.
- Use `any`. Use `unknown` and narrow it.

## Style

- Components in PascalCase files, everything else in kebab-case.
- Tailwind classes only. No inline `style` and no new CSS files.
- Prettier handles formatting. Don't hand-format.

## Before you finish

1. `pnpm lint` passes.
2. `pnpm exec tsc --noEmit` passes.
3. `pnpm test` passes.
4. `pnpm build` succeeds if you touched routing, config or server actions.
5. List the files you changed and any page you couldn't check in the browser.

## Never

- Commit `.env*` files except `.env.example`.
- Run migrations against anything but the local database.
- Change `next.config.ts` or `middleware.ts` without asking.
- Force push or push to `main`.
