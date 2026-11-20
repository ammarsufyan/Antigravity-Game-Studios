# Security Policy

## Supported Versions

Security fixes apply to the latest release on `main`. Older releases are not supported.

## Reporting a Vulnerability

**Do not report security vulnerabilities through public GitHub issues.**

Use GitHub's private vulnerability reporting instead:

**[Report a vulnerability →](https://github.com/ammarsufyan/Antigravity-Game-Studios/security/advisories/new)**

Include as much detail as possible:
- Description of the vulnerability and what it affects
- Steps to reproduce
- Potential impact and attack scenarios
- Any suggested mitigations

**What to expect:**
- Acknowledgment within **48 hours**
- Status update within **7 days**
- Resolution within **90 days** for confirmed vulnerabilities

## What Is In Scope

Antigravity Game Studios is a **local development template** — it defines agent instructions, skills, rules, and optional helper scripts that run directly in your workspace. Security issues are primarily about contributed files that could execute unintended commands or exfiltrate secrets on a user's machine.

### High Severity
- Helper scripts (`.agents/scripts/*`) that execute malicious or undisclosed shell commands on user machines
- Skills, rules, or agents that exfiltrate environment variables, API keys, or secrets
- Prompt injection via skill, rule, or agent definitions that causes Antigravity to bypass safety measures or take unauthorized destructive actions
- Contributions that silently alter behavior in ways users cannot audit

### Medium Severity
- Skills that make undisclosed outbound network requests
- Agent definitions that escalate tool permissions or bypass user confirmation prompts
- Scripts that behave differently across OSes to conceal behavior
- Skills that write outside their documented scope without explicit user approval

### Out of Scope
- The behavior of Google Antigravity or its underlying AI models (report to Google Security)
- Bugs in the user's local Antigravity installation, OS, or game engine
- Theoretical vulnerabilities with no realistic attack path
- Issues requiring physical access to the user's machine

## Security Guidelines for Contributors

When contributing skills, agents, rules, or scripts:

- **Scripts must be transparent and POSIX-compatible** — use `grep -E`, not `grep -P`; avoid obfuscated shell constructs
- **No silent network calls** from scripts or skills unless explicitly documented and opt-in
- **No reading secrets or environment variables** beyond what is minimally required and clearly documented
- **Skills must not write outside their documented scope** without explicit user confirmation

## Disclosure Policy

We follow a **90-day coordinated disclosure** timeline:

1. You submit the vulnerability privately
2. We acknowledge within 48 hours
3. We confirm and assess severity within 7 days
4. We develop and test a fix
5. We notify you before any public disclosure
6. Public disclosure happens after the fix ships, or at 90 days — whichever comes first

We credit reporters in release notes unless you prefer to remain anonymous.
