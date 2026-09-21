# github-workflows

## snapshot-test

The reusable composition test workflow restores schema caches before testing.
`test_target` selects a single Make target (default `test`); set `validate: false` when that target already performs blocking validation.
Call it in separate jobs with different targets for quick feedback and full lifecycle checks.
Optional `artifact_path` and `artifact_name` retain test evidence for seven days. Only opt in with synthetic, non-sensitive test output.

## crossplane

Build and push a crossplane package

### Usage

```yaml
on:
  push:
    tags:
      - "v*"
jobs:
  publish-crossplane-package:
    uses: sn-atmos/github-workflows/.github/workflows/crossplane.yaml@main
```
