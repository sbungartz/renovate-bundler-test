# renovate-bundler-test

Reproduce issue with Renovate using `bundler` and `"rangeStrategy": "update-lockfile"`:

- There are Patch- and Major-Updates available for the dependency `js-routes`.
- Renovate correctly identifies this and creates two PRs, one for the non-major, and one for the major update.
- In the non-major PR, it claims in the description to update from `1.4.9` to `1.4.14` but looking at the `Gemfile.lock` reveals that it has actually updated to `2.2.4`

Looking at the log shows that the following command is executed:
```
bundler lock --update js-routes
```

This command will always update to the latest version permitted by the `Gemfile`, so will perform the major update in any case.
