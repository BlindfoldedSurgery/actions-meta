# actions-releases

This repository contains a set of reusable workflows geared towards supporting the release process
of a versioned project.

The project follows semantic versioning. You can depend on tags for specific versions of use a
major version tag (e.g. `v1`).

Every commit on the main branch leads to a new release. Releases are managed by
[commitizen][commitizen], which relies on [conventional commits][ccommit]. To make sure you don't
accidentally create commits with an unconventional message, install a pre-commit hook using
`make pre-commit`.

[commitizen]: https://commitizen-tools.github.io/commitizen/

[ccommit]: https://www.conventionalcommits.org/en/v1.0.0/

## Example

```yaml
jobs:
  commitizen:
    uses: BlindfoldedSurgery/actions-releases/.github/workflows/commitizen.yml@v1
    with:
      python-version: '3.12'
```

## Available Workflows

### commitizen-check

Checks whether commit messages in a PR abide by the [conventional commit][ccommit] rules.

**Inputs:**

| Name           | Required | Default |     Example      | Description                                      |
|:---------------|:--------:|:-------:|:----------------:|--------------------------------------------------|
| python-version |    no    | `3.11`  | `3.12`, `3.12.1` | The Python version with which to run commitizen. |

### commitizen-bump

Invokes cz bump for changes on the default branch and creates an (auto-merged) PR with the bump.

**Inputs:**

| Name              | Required | Default |     Example      | Description                                      |
|:------------------|:--------:|:-------:|:----------------:|--------------------------------------------------|
| publish-major-tag |    no    | `false` |  `true`/`false`  | Whether to publish a major tag (e.g. `v1`).      |
| python-version    |    no    | `3.11`  | `3.12`, `3.12.1` | The Python version with which to run commitizen. |

**Secrets:**

| Name       | Required | Description                                                                      |
|:-----------|:--------:|----------------------------------------------------------------------------------|
| `GH_TOKEN` |   yes    | A GitHub personal access token that can create PRs and read/write repo contents. |

### commitizen-version

Provides the current project version as a `version` output.

**Inputs:**

| Name           | Required | Default |     Example      | Description                                      |
|:---------------|:--------:|:-------:|:----------------:|--------------------------------------------------|
| python-version |    no    | `3.11`  | `3.12`, `3.12.1` | The Python version with which to run commitizen. |
