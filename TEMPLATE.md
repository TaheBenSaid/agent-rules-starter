# `<Project name>`

## Project

<One paragraph. What this is, who uses it, and the stack. For example: "Mobile app for booking
fitness classes. Flutter 3, Bloc for state, REST backend we don't own. Ships to iOS and Android.">

## Commands

Run these exactly. Don't guess other ones.

- Install: `<install command>`
- Run: `<run command>`
- Test: `<test command>`
- Test one file: `<single test command> <path>`
- Lint: `<lint command>`
- Format: `<format command>`
- Build: `<build command>`

## Architecture

- `<folder>/`: `<what lives here>`
- `<folder>/`: `<what lives here>`
- `<folder>/`: `<what lives here>`
- New `<feature, route or module>` goes in `<path>`, following `<existing example path>`.
- Generated files: `<pattern>`. Never edit them by hand. Regenerate with `<command>`.

## Rules

Do:

- <One line, checkable. For example: "Use the logger in `src/lib/log.ts`, never `console.log`.">
- <One line, checkable.>
- <One line, checkable.>

Don't:

- <One line, checkable. For example: "Don't add a dependency without asking first.">
- <One line, checkable.>
- <One line, checkable.>

## Style

- <Naming rule. For example: "Files in kebab-case, classes in PascalCase.">
- <Formatting is handled by `<formatter>`. Don't hand-format.>
- <Comments explain why, not what.>
- <Error handling, for example: "Never swallow an error. Log it or return it.">

## Before you finish

Run these and fix what you broke. Report the result of each.

1. `<lint command>` passes with no new warnings.
2. `<test command>` passes.
3. `<build or type check command>` succeeds.
4. <Manual check, for example: "Open the changed screen and check it in dark mode.">
5. List the files you changed and anything you couldn't verify.

## Never

- Commit secrets, `.env` files, keys or tokens. Read config from `<config location>`.
- Force push, rewrite history, or push to `<main branch>` directly.
- Touch production config: `<paths>`.
- Run migrations or scripts against a real database.
- Delete files outside the task you were given.
