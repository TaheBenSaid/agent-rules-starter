---
name: agent-rules-starter
description: Write an AGENTS.md or CLAUDE.md for a repo so coding agents follow the project's commands and rules. Use when the user asks to set up agent rules, create AGENTS.md, CLAUDE.md, copilot-instructions.md or Cursor rules, or says the agent keeps ignoring how the project works.
---

# Agent rules starter

The template is `TEMPLATE.md` in this skill's folder. Filled examples for common stacks are in `examples/`.

## Steps

1. Check what's already there: `AGENTS.md`, `CLAUDE.md`, `.github/copilot-instructions.md`, `.cursor/rules/`, `.cursorrules`. If one exists, improve it instead of starting over, and keep the user's rules.

2. Inspect the repo. Read, don't guess:
   - package files: `package.json`, `pubspec.yaml`, `pyproject.toml`, `build.gradle(.kts)`, `go.mod`, `Cargo.toml`, `Gemfile`
   - scripts: the `scripts` block, `Makefile`, `justfile`, `Taskfile.yml`
   - the lockfile, to pick the right package manager
   - lint and format config: `.eslintrc*`, `eslint.config.*`, `analysis_options.yaml`, `ruff.toml`, `.editorconfig`, ktlint or detekt config
   - CI files under `.github/workflows/` or similar. CI shows which commands the team trusts.
   - the top two levels of folders, plus one existing feature, to see where code goes
   - generated files and how they get regenerated
   - `.gitignore` and `.env.example`, to see what's secret

3. Run the commands you plan to list, at least lint and test. Only list commands that worked, or that you can see running in CI. If one fails for a reason unrelated to the setup, say so to the user instead of dropping it silently.

4. Draft the file from `TEMPLATE.md`. If an example in `examples/` matches the stack, use it as a reference for tone and detail, not as content. Every rule is one line and checkable from a diff. Drop sections that would be empty. Aim for under 100 lines.

5. Ask the user at most three short questions, only about things the code can't tell you. Good ones:
   - "Any mistakes you keep correcting in review?"
   - "Anything the agent must never touch, like prod config or a vendored folder?"
   - "Should it ask before adding dependencies?"
   Skip any question the repo already answers.

6. Write the file. Default to `AGENTS.md` at the repo root. Use `CLAUDE.md` if that's the only tool the user mentioned.

7. Offer the symlink so other tools read the same file:

   ```bash
   ln -s AGENTS.md CLAUDE.md
   mkdir -p .github && ln -s ../AGENTS.md .github/copilot-instructions.md
   ```

   On Windows, or if the user prefers no symlinks, a `CLAUDE.md` that only contains `@AGENTS.md` works for Claude Code.

8. Don't commit. Show the file path, the line count, and which commands you verified.

## Rules for the file itself

- Exact commands in backticks, copied from the repo.
- No secrets, tokens or internal URLs. The file gets committed.
- Nothing the linter already enforces.
- No vague rules like "write clean code". Rewrite them into something checkable or cut them.
