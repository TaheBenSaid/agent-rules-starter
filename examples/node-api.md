# Parcel API

## Project

REST API for a delivery tracking product. Node 22, TypeScript, Fastify, Postgres with
Prisma. Mobile and web clients both depend on it, so response shapes are a contract.
Package manager is npm.

## Commands

- Install: `npm ci`
- Dev server: `npm run dev` (http://localhost:4000)
- Test: `npm test` (Vitest, needs `docker compose up -d db` first)
- Test one file: `npx vitest run src/routes/shipments/shipments.test.ts`
- Lint: `npm run lint`
- Type check: `npx tsc --noEmit`
- Build: `npm run build`
- New migration: `npx prisma migrate dev --name <short_name>`
- Regenerate client: `npx prisma generate`

## Architecture

- `src/routes/<resource>/`: route file, zod schemas and tests for one resource.
- `src/services/`: business logic. Routes call services, services call Prisma.
- `src/plugins/`: Fastify plugins for auth, rate limiting and error handling.
- `src/lib/errors.ts`: the only place HTTP error shapes are defined.
- `prisma/schema.prisma`: database schema. Migrations in `prisma/migrations/` are generated.

## Rules

Do:

- Define request and response schemas with zod for every route.
- Return errors through `AppError` from `src/lib/errors.ts`.
- Put queries in services, never in route handlers.
- Use the request logger (`req.log`), not `console.log`.
- Add a test for every new route: one success case, one validation failure.

Don't:

- Rename or remove a field in a response. Add a new field instead.
- Edit an existing migration. Create a new one.
- Log tokens, passwords, or full request bodies.
- Add a dependency without asking.

## Style

- Files in kebab-case. One route file per resource.
- `async`/`await` only. No `.then` chains.
- Comments explain why, not what.

## Before you finish

1. `npm run lint` passes.
2. `npx tsc --noEmit` passes.
3. `npm test` passes.
4. If you changed the schema, a new migration exists and `npx prisma generate` ran.
5. List the files you changed and any endpoint whose response shape changed.

## Never

- Commit `.env` or anything under `secrets/`.
- Run `prisma migrate reset` or `prisma db push` against anything but the local database.
- Touch `deploy/` or the production Dockerfile without asking.
- Force push or push to `main`.
