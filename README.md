# github-workflows

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
