## Summary

- Briefly describe the wrapper-facing change.

## Scope

- [ ] Wrapper metadata or README only
- [ ] Release notes or contribution docs
- [ ] Workflow, dependency, or publishing change

## Safety Check

- [ ] No real secrets, tokens, cookies, private paths, or internal URLs were added.
- [ ] Scanner behavior changes belong in `aolingge/agent-secret-guard`, not this wrapper.
- [ ] Publishing or dependency changes are called out for maintainer review.

## Verification

```bash
git diff --check
node E:/codemain/github/agent-secret-guard/dist/cli.js scan . --fail-on high
```
