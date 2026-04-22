# Changelog

All notable changes to `agent-secret-guard-action` are documented here.

The action wrapper is intentionally small. Scanner rules, CLI behavior, and remediation docs live in the main [`agent-secret-guard`](https://github.com/aolingge/agent-secret-guard) repository.

## v0.1.4 - 2026-04-21

- Pins the wrapper to `agent-secret-guard@0.2.3`.
- Documents text, JSON, and SARIF output options.
- Keeps the Marketplace action focused on CI usage while linking back to the main scanner repository.

## Release Notes Template

Use this for the next wrapper release:

````markdown
## Agent Secret Guard Action vNEXT

This release updates the GitHub Actions wrapper for `agent-secret-guard`.

Wrapper changes:

- <short wrapper change>

Scanner package:

- Uses `agent-secret-guard@<version>`.
- Scanner release notes: https://github.com/aolingge/agent-secret-guard/releases

Quick start:

```yaml
- uses: aolingge/agent-secret-guard-action@vNEXT
  with:
    path: .
    fail-on: high
```
````
