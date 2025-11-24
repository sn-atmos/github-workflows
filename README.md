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

## release-please

A handy workflow for jobs that rely on tags. This automates tags and changelog generation based on conventional commits. Read more about this [here](https://github.com/googleapis/release-please)

### Usage

```yaml
on:
  push:
    branches:
      - main
jobs:
  release:
    uses: sn-atmos/github-workflows/.github/workflows/release-please.yaml@main
    secrets: inherit
```

Check [release-please.yaml](.github/workflows/release-please.yaml#L6) for inputs

### Release-please administration notes

You only need to read this if you are setting up Release Please Github App and organization secret yourself.

By default, release-please uses `GITHUB_TOKEN`, but this will not trigger additional workflows like `publish-docker-image` in this case [[source](https://github.com/googleapis/release-please-action?tab=readme-ov-file#github-credentials)]

So that "release-please" PR's can trigger additional workflows, we use the action `actions/create-github-app-token` to create a token based on github app app credentials.

```sh
      - uses: actions/create-github-app-token@v1
        id: app-token
        with:
          app-id: ${{ inputs.appID }}
          private-key: ${{ secrets.RELEASE_BOT_PRIVATE_KEY }}
```

For convenience, the `RELEASE_BOT_PRIVATE_KEY` is set up as an organization level [actions secret](https://github.com/organizations/sn-atmos/settings/secrets/actions). `inputs.appID` defaults to the bot id in this organisation.

**App config**:

**1:** create personal or [organization github app](https://github.com/organizations/sn-atmos/settings/installations)

**2:** use the following permissions:

- Metadata - readonly (mandatory)
- Contents - read/write
- Pull Requests - read/write
- Issues - read/write

**3:** note app-id

**4:** create/download private-key

- its stored in ~/downloads (depending on browser/settings)

**5:** update project [actions secret](https://github.com/organizations/sn-atmos/settings/secrets/actions) and variables(or reusable workflow input default value)

**release-please required permissions**

```yaml
permissions:
  contents: write
  pull-requests: write
  issues: write
```
