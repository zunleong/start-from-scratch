<<<<<<< HEAD
# Start From Scratch

A Claude Skill that turns "start a new website project" into a guided, best-practice-driven setup instead of a blank terminal.

Instead of guessing your stack, it runs a short live interview (project type, framework, language, exact versions, build approach, styling), gives you best-practice advisory notes based on what you picked, then shows the **full plan and exact commands** and waits for your explicit go-ahead before creating anything.

## Why

Kicking off a new frontend project usually means re-deciding the same things every time — Vite vs. a meta-framework, Tailwind vs. Sass, whether to bother with linting — and either forgetting a step or copy-pasting from the last project. This skill encodes that decision process once, asks it consistently, and never touches your filesystem without confirmation.

## What it does

1. Asks: project type, framework, language, exact framework/language version, build approach (SPA vs SSR, if relevant), styling approach, target folder, and whether to `git init`
2. Surfaces short best-practice notes based on your specific combination of answers (e.g. suggesting Pinia for a Vue 3 dashboard, or `strict: true` for TypeScript) — informational only, nothing is auto-installed
3. Shows the complete plan (stack, versions, folder, and the exact commands it's about to run) and waits for a clear **yes**
4. Only then scaffolds the project, sets up ESLint + Prettier, initializes git if requested, and lays out a folder structure sized to the project type

**Fixed defaults, never asked:** npm as the package manager, ESLint + Prettier always configured, no test framework, no extra libraries pre-installed (routing/state management/UI kits are mentioned as suggestions only).

## Installation

### Claude.ai (web/desktop/mobile)
1. Download [`start-from-scratch.zip`](https://github.com/zunleong/start-from-scratch/releases) from the latest [release](https://github.com/zunleong/start-from-scratch/releases) (or zip the `start-from-scratch/` folder yourself)
2. In Claude.ai, go to **Settings → Features → Skills**
3. Upload the zip — make sure code execution is enabled in Settings → Capabilities
4. Enable the skill

### Claude Code
Clone this repo, then copy (or symlink) the skill folder into your skills directory:
```bash
# Personal, available in every project
cp -r start-from-scratch ~/.claude/skills/

# Or project-only
cp -r start-from-scratch /path/to/your/project/.claude/skills/
```

## Usage

Just say something like:
- "Start a new project from scratch"
- "Scaffold a new website"
- "Set up a new frontend app"

The skill runs its interview, shows you the plan, and waits for confirmation before doing anything.

## Versioning

This project follows [Semantic Versioning](https://semver.org/). See [CHANGELOG.md](./CHANGELOG.md) for release history.

- **Patch** (1.0.x): wording fixes, small corrections, no behavior change
- **Minor** (1.x.0): new questions, new advisory notes, new reference files, backward-compatible additions
- **Major** (x.0.0): changes to the interview flow or confirmation behavior that change how the skill acts

Current version: **1.0.0**

## Contributing / updating your own copy

This started as a personal skill, so there's no formal contribution process yet — but issues and PRs with suggestions (extra advisory notes, framework coverage, etc.) are welcome. If you fork it for your own use, feel free to strip or extend the best-practice notes to match your own conventions.

## License

MIT — see [LICENSE](./LICENSE).
=======
# start-from-scratch
>>>>>>> 9ec8823257250454f0cd96450347a88b82b21c9a
