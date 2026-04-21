# Agent Secret Guard Action

Run `agent-secret-guard` in GitHub Actions to scan AI agent, MCP, and local automation repositories for risky secrets and permissions.

This wrapper action is intentionally small. The scanner source, rules, docs, and examples live in the main repository:

- Main repo: <https://github.com/aolingge/agent-secret-guard>
- npm package: <https://www.npmjs.com/package/agent-secret-guard>
- Fix guide: <https://github.com/aolingge/agent-secret-guard/blob/main/docs/remediation.md>

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
      - uses: aolingge/agent-secret-guard-action@v0.1.4
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
- uses: aolingge/agent-secret-guard-action@v0.1.4
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

## What It Catches

- MCP tokens passed through command args.
- Hardcoded API and package tokens.
- Broad filesystem access in agent or automation configs.
- Browser profile and credential store exposure.
- Dangerous shell commands in agent instructions.
- Over-permissive GitHub Actions workflows.

## Privacy

The action runs the npm CLI package inside your workflow. It does not upload findings to a remote service. Treat text, JSON, and SARIF reports as sensitive artifacts because they may include private file paths or surrounding evidence.

## License

MIT
