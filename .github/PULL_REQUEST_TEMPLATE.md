## Summary

Brief description of what this PR does.

## Type of Change

- [ ] New agent
- [ ] New skill
- [ ] New rule or script
- [ ] Bug fix
- [ ] Documentation improvement
- [ ] Other:

## Changes

-
-
-

## Checklist

- [ ] I've tested this in a Google Antigravity session (App, IDE, or `agy` CLI)
- [ ] New agents use Antigravity frontmatter (`name`, `description`, `subagent: true`, `mainAgent: false`, native `tools`) and include a Collaboration Protocol section
- [ ] New skills use the subdirectory format (`.agents/skills/<name>/SKILL.md`) with valid `name` and `description` frontmatter only
- [ ] New rules use `trigger: glob` with quoted, brace-expanded, `**/`-prefixed `globs:`
- [ ] Reference docs are updated (`agent-roster.md`, `skills-reference.md`, `rules-reference.md`)
- [ ] Cross-platform compatible on Windows (without requiring Bash/Python), macOS, and Linux
- [ ] No hardcoded paths or platform-specific assumptions
