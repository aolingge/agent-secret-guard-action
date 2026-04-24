# Agent Secret Guard Action

Run `agent-secret-guard` in GitHub Actions to scan AI agent, MCP, and local automation repositories for risky secrets and permissions.

[![GitHub Marketplace](https://img.shields.io/badge/GitHub%20Marketplace-Agent%20Secret%20Guard-blue?logo=github)](https://github.com/marketplace/actions/agent-secret-guard)
[![Main repo](https://img.shields.io/badge/Main%20repo-agent--secret--guard-0f172a?logo=github)](https://github.com/aolingge/agent-secret-guard)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

This wrapper action is intentionally small. The scanner source, rules, docs, and examples live in the main repository:

- Marketplace listing: <https://github.com/marketplace/actions/agent-secret-guard>
- Main repo: <https://github.com/aolingge/agent-secret-guard>
- npm package: <https://www.npmjs.com/package/agent-secret-guard>
- Fix guide: <https://github.com/aolingge/agent-secret-guard/blob/main/docs/remediation.md>
- Changelog: [CHANGELOG.md](CHANGELOG.md)

## Quick Start

```yaml
name: Agent Secret Guard

on:
  pull_request:
  push:
    branches: [main]

permissions:
  contents: read

jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6
      - uses: aolingge/agent-secret-guard-action@v0.1.5
        with:
          path: .
          fail-on: high
```

## Inputs

| Input | Default | Description |
| --- | --- | --- |
| `path` | `.` | Directory or file to scan. |
| `fail-on` | `high` | Lowest severity that should fail the action: `low`, `medium`, `high`, or `critical`. |
| `format` | `text` | Output format: `text`, `json`, or `sarif`. |
| `output` | empty | Optional file path to write the report to. |

## SARIF Example

```yaml
- uses: aolingge/agent-secret-guard-action@v0.1.5
  with:
    path: .
    fail-on: high
    format: sarif
    output: agent-secret-guard.sarif

- uses: github/codeql-action/upload-sarif@v4
  if: always()
  with:
    sarif_file: agent-secret-guard.sarif
```

## Version Policy

Each action tag pins a specific `agent-secret-guard` npm package version inside `action.yml`. This keeps workflow runs reproducible.

To get scanner rule updates, upgrade the action tag after checking the wrapper [changelog](CHANGELOG.md) and the main scanner [release notes](https://github.com/aolingge/agent-secret-guard/releases).

## What It Catches

- MCP tokens passed through command args.
- Hardcoded API and package tokens.
- Broad filesystem access in agent or automation configs.
- Browser profile and credential store exposure.
- Dangerous shell commands in agent instructions.
- Over-permissive GitHub Actions workflows.

## Privacy

The action runs the npm CLI package inside your workflow. It does not upload findings to a remote service. Treat text, JSON, and SARIF reports as sensitive artifacts because they may include private file paths or surrounding evidence.

## Contributing

Wrapper changes are documented in [CONTRIBUTING.md](CONTRIBUTING.md). Scanner rule changes should go to the main [`agent-secret-guard`](https://github.com/aolingge/agent-secret-guard) repository.

## License

MIT

## Support

Report wrapper execution bugs with the [bug report form](https://github.com/aolingge/agent-secret-guard-action/issues/new?template=bug_report.yml). Scanner rule requests and false-positive reports belong in the main [`agent-secret-guard`](https://github.com/aolingge/agent-secret-guard) repository.

If this project saves you time, you can support future maintenance here: [Buy Me a Coffee](https://www.buymeacoffee.com/aolingge).
