# Contributing to Antigravity Game Studios

Antigravity Game Studios (AGS) is a native Google Antigravity coordination template for indie game development.
Contributions are welcome — bug fixes, new skills that fill a real gap, agent improvements, rule refinements, and cross-platform helper improvements. PRs that don't fit the template's direction may be closed without lengthy explanation.

## What Makes a Good PR

- **Bug fixes** — something is broken, here's the fix
- **New skills** that address a workflow gap not already covered
- **Improvements** to existing agents, skills, rules, or cross-platform scripts
- **Documentation corrections** — wrong info, broken references, outdated steps

Feature requests submitted as PRs will be closed. Open an issue instead.

**What this repo isn't:**
Antigravity Game Studios is the template that helps you build games, not a place to store the games you build with it. GDDs, ADRs, game concepts, level designs, narrative docs, or game source code generated for your own project belong in your own repo.

## The Non-Negotiable Technical Rules

These are the things that will get your PR rejected if you miss them.

**Skill files**
- Skills live in `.agents/skills/<name>/SKILL.md` — the subdirectory format is required.
- `SKILL.md` YAML frontmatter must contain only `name` (exact match to the folder name) and a non-empty `description`.
- Never use inline shell execution syntax in Markdown; instruct Antigravity to read `project.yaml` / `project.local.yaml` with `read_file` or run commands via `run_command` with a Windows fallback.

**Agent files**
- Agents live in `.agents/agents/<name>.md`.
- Frontmatter must include `name`, `description`, `subagent: true`, `mainAgent: false`, and an explicit native Antigravity `tools:` list (`read_file`, `edit_file`, `write_file`, `run_command`, `manage_task`, `search_web`, `invoke_subagent`, `send_message`).
- New agents must include a **Collaboration Protocol** section that describes how the agent asks questions and defers decisions to the user.
- Agents must not modify files outside their documented domain without explicit user delegation.

**Rule files**
- Rules live in `.agents/rules/<name>.md` and must stay under 24,000 bytes.
- Path-scoped rules must use `trigger: glob` with a quoted, comma-separated, brace-expanded, `**/`-prefixed `globs:` string.
- Hierarchical `AGENTS.md` files must be plain Markdown with no YAML frontmatter.

**Optional helper scripts (`.agents/scripts/`)**
- Shell scripts must use LF (`\n`) line endings and POSIX-compatible patterns (`grep -E`, never `grep -P`).
- Every skill invoking a `.sh` script must include a fallback so Windows users without Git Bash or Python are never blocked.

**Reference docs**
- If your PR adds or changes a skill, agent, or rule, update the matching reference doc (`agent-roster.md`, `skills-reference.md`, or `rules-reference.md`).

## The Collaborative Principle

Antigravity Game Studios is not an autonomous system. Every workflow follows:
**Question -> Options -> Decision -> Draft -> Approval -> Write**

Skills and agents must ask before acting. Nothing writes to game files without explicit user confirmation (respecting `modes.automation` in `project.yaml`).

## Testing Your Changes

Run your change in a Google Antigravity session and confirm it works end-to-end. For skills, invoke the skill and verify the output matches what the skill claims to do. For agents or rules, verify valid YAML frontmatter and LF line endings.

Include a brief note in your PR description describing what you tested and what the output looked like.

## Commit Format

Use [Conventional Commits](https://www.conventionalcommits.org/):

```text
feat: add /retrospective skill for end-of-sprint reviews
fix: correct cross-platform fallback in /project-settings
docs: update skills-reference with new /qa-plan entry
```

Types: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`

## PR Process

- Your PR will be auto-assigned to `@ammarsufyan` via `CODEOWNERS`
- Reviews happen as maintainer bandwidth allows
- Merged contributors are credited in release notes

## Platform Compatibility

Antigravity Game Studios must work natively on **Windows (without requiring Git Bash or Python), macOS, and Linux**. Never introduce mandatory Unix-only dependencies into skills or rules.
