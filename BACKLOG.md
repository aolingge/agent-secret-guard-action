# Backlog

## Governance

- 2026-07-10: Review Dependabot PR #6 (`actions/checkout` 6.0.2 -> 7.0.0). Read-only checks showed the PR remains open and recent repository workflows are successful, but `gh pr checks 6` still reports no checks on the Dependabot branch. The local ahead commit `266233a` already adds a v7 wrapper smoke check, so merge, push, and GitHub/Gitee sync still require maintainer review plus explicit authorization.
