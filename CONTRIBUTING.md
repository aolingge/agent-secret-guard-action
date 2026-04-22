# Contributing

Thanks for improving `agent-secret-guard-action`.

This repository is a thin GitHub Actions wrapper. Most scanner behavior belongs in the main [`agent-secret-guard`](https://github.com/aolingge/agent-secret-guard) repository.

## What Belongs Here

- Action metadata and input documentation.
- Marketplace-focused README improvements.
- Wrapper release notes.
- CI examples for running the published scanner in GitHub Actions.

## What Belongs In The Main Scanner Repo

- Detection rules.
- CLI flags and output formats.
- Remediation guidance.
- Test fixtures for safe or unsafe agent, MCP, and automation configs.

## Safety Rules

- Do not include real secrets, tokens, cookies, browser profile paths, internal URLs, or private filesystem paths.
- Redact scan output before sharing it in issues or pull requests.
- Treat workflow, publishing, dependency, and authentication changes as security-sensitive.
- Keep pull requests small and include verification commands.

## Local Checks

From this repository:

```bash
git diff --check
node E:/codemain/github/agent-secret-guard/dist/cli.js scan . --fail-on high
```

If the main scanner repository is not available locally, use the published package:

```bash
npx agent-secret-guard scan . --fail-on high
```
