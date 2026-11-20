# agent-rules-starter

The one file that makes your AI coding agent follow your rules.

Every coding agent reads a plain markdown file from your repo before it starts work. Put your commands, your folder layout and your rules in it, and the agent stops guessing. Leave it out, and you explain the same things in every chat.

This repo has a template for that file, five filled examples, and a skill that writes one for your project by reading the code.

## Where each tool looks

| File | Read by |
| --- | --- |
| `AGENTS.md` | OpenAI Codex, Cursor, and a growing list of other agents |
| `CLAUDE.md` | Claude Code |
| `.github/copilot-instructions.md` | GitHub Copilot |
| `.cursor/rules/*.mdc` | Cursor project rules (markdown with a small frontmatter block) |

The first two sit at the repo root. Support changes often, so check your tool's docs if something isn't picked up.

## The idea

Short, specific, testable rules beat long essays.

"Write clean code" does nothing. "Run `pnpm lint` before you finish" does. A good rule is one line, and you can check whether the agent followed it by reading the diff. If you can't check it, cut it or rewrite it.

Aim for under 100 lines. The agent reads the whole file every time, so every line costs attention.

## Quick start

```bash
git clone https://github.com/TaheBenSaid/agent-rules-starter.git
cp agent-rules-starter/TEMPLATE.md your-project/AGENTS.md
```

Then edit five things:

1. **Project.** One paragraph: what it is and the stack.
2. **Commands.** The exact install, run, test, lint and build commands. Copy them from `package.json`, `Makefile` or CI, and run each one once.
3. **Architecture.** Where things live and where new code goes.
4. **Rules.** The mistakes you keep correcting in review. One line each.
5. **Before you finish.** The checks the agent runs before it says it's done.

Delete every section you don't need. If your stack is in [`examples`](examples), start from that one instead:

- [`flutter-app.md`](examples/flutter-app.md)
- [`nextjs-app.md`](examples/nextjs-app.md)
- [`node-api.md`](examples/node-api.md)
- [`python-service.md`](examples/python-service.md)
- [`android-kotlin.md`](examples/android-kotlin.md)

## What to put in

- Exact commands, including how to run a single test.
- Paths: where features live, which files are generated.
- The rules a new teammate would break in their first week.
- What "done" means: lint, tests, build, a manual check.
- What's off limits: secrets, prod config, force push.

## What to leave out

- Things your linter or formatter already enforces.
- Long explanations of why. One clause is enough.
- Your whole architecture doc. Link to it.
- Rules nobody can check, like "be thoughtful".
- Secrets, tokens and internal URLs. This file gets committed.

## One file for several tools

Keep `AGENTS.md` as the real file and point the others at it:

```bash
ln -s AGENTS.md CLAUDE.md
mkdir -p .github && ln -s ../AGENTS.md .github/copilot-instructions.md
```

Git stores symlinks fine on macOS and Linux. On Windows, check that `core.symlinks` is on, or skip the symlink and put a single line in `CLAUDE.md` that says `@AGENTS.md`. Claude Code reads that as an import.

## Use it as a skill

Clone it into your agent's skills folder, for example:

```bash
git clone https://github.com/TaheBenSaid/agent-rules-starter.git ~/.claude/skills/agent-rules-starter
```

Then ask "set up agent rules for this repo" or "write an AGENTS.md". The agent reads your package files, scripts, lint config and CI, fills the template with commands it actually ran, asks you up to three questions about rules it can't work out from the code, and writes the file.

## More tools

Part of a series of small tools I use on real projects, each tied to something I write about. The full list is in [flutter-skills](https://github.com/TaheBenSaid/flutter-skills).

## License

MIT
