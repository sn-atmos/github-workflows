# github-workflows

## release-please

A handy workflow for jobs that rely on tags. This automates tags and changelog generation based on conventional commits. Read more about this [here](https://github.com/googleapis/release-please)

```yaml

```

Check [release-please.yaml](.github/workflows/release-please.yaml#L6) for inputs

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

Check [crossplane.yaml](.github/workflows/crossplane.yaml#L6) for inputs

## git-tag

Tag a ref

### Usage

Automatically update the dev-tag on push to main:

```yaml
---
name: Deploy to Dev

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  tag-dev:
    uses: sn-atmos/github-workflows/.github/workflows/git-tag.yaml@main
    with:
      tag_name: dev
      ref: ${{ github.sha }}
```

Check [git-tag.yaml](.github/workflows/git-tag.yaml#L6) for inputs
