# CSA Repository Standards

Standard configuration and best practices for Cloud Security Alliance GitHub repositories. This is a living document — update it as standards evolve.

## Branch Protection

All repositories with active development should use **GitHub rulesets** (preferred over classic branch protection) on their default branch.

### Minimum ruleset for `main`

| Setting | Value | Notes |
|---------|-------|-------|
| Require PR before merging | Yes | No direct pushes to main |
| Required approving reviews | 1 | Higher for security-critical repos |
| Dismiss stale reviews on push | Yes | Prevents approve-then-sneak-changes |
| Require code owner review | Optional | Enable when CODEOWNERS file exists |
| Org admin bypass | Allowed | For practicality on small teams |

### Storing ruleset config

Each repo should store its ruleset configuration in `.github/rulesets/<name>.json`. This serves as documentation of intent and makes it easy to reproduce the setting on new repos. Strip API metadata (`_links`, `node_id`, etc.) — just keep the configuration that matters.

## Merge Strategy

| Setting | Recommendation |
|---------|----------------|
| Allowed merge methods | Merge, squash, rebase (all allowed) |
| Default for most PRs | Squash and merge (clean history) |
| Auto-delete head branches | Enable (prevents branch clutter) |

## Status Checks (Planned)

Not yet required. When added, these should include:

- **Linting** — ShellCheck for bash scripts, PSScriptAnalyzer for PowerShell
- **Syntax validation** — `bash -n` for shell scripts
- **Security scanning** — Semgrep or similar

## Repository Settings

| Setting | Value |
|---------|------|
| Default branch | `main` |
| Issues | Enabled |
| Wiki | Disabled (use docs in repo) |
| Sponsorships | Disabled |
| Projects | Org-level only |

## Issue & PR Templates

Repos with external contributors should include issue templates in `.github/ISSUE_TEMPLATE/. See [DesktopSetup](https://github.com/CloudSecurityAlliance/DesktopSetup/tree/main/.github/ISSUE_TEMPLATE) for examples.

## Security

- See [SECURITY.md](SECURITY.md) for the org-level security policy
- Never commit secrets, credentials, or API keys
- Use GitHub Secrets for CI/CD values

## Future Standards

These are planned but not yet implemented:

- [ ] CODEOWNERS files for automatic review assignment
- [ ] Required status checks (linting, security scanning)
- [ ] Automated dependency updates (Dependabot / Renovate)
- [ ] Commit signing requirements
- [ ] Branch naming conventions
- [ ] PR size guidelines
