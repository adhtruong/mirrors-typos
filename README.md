# mirrors-typos

Mirror of [typos](https://github.com/crate-ci/typos) for pre-commit.

## Why use this mirror?

The original `typos` repository uses multiple tagging strategies:

- A mutable `v1` tag
- Semantic release tags (e.g., `v1.3.3`)
- Subpackage tags (e.g., `typos-v0.8.2`)

When using `pre-commit autoupdate`, this causes confusion because pre-commit's autoupdate can switch between different project tags in the same repository. For example, it might incorrectly update from `v1.3.1` to `typos-v0.8.2` instead of the latest semantic release like `v1.3.3`.

This mirror repository solves this problem by filtering and only mirroring `v1.*` semantic release tags, ensuring `pre-commit autoupdate` works correctly and always updates to the proper semantic version.

See [GitHub issue #390](https://github.com/crate-ci/typos/issues/390) for the original discussion.

## Usage

Add this to your `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/adhtruong/mirrors-typos
    rev: v1.42.0  # Use the latest version from the releases page
    hooks:
      - id: typos
```

To find the latest version, check the [releases page](https://github.com/adhtruong/mirrors-typos/releases) or run `pre-commit autoupdate` which will automatically update to the latest available version.

For additional configuration options, refer to the [typos documentation](https://github.com/crate-ci/typos).

## Differences from typos pre-commit

- **Only binary installation**: Only the `typos` binary is supported (no additional stages configuration)
- **Simplified hook configuration**: The `stages` parameter is not specified in the hook definition, as this is not supported by the mirror generation tool

## Maintenance

This mirror is automatically maintained via GitHub Actions. The workflow runs daily and on pushes to the main branch, using [pre-commit-mirror-maker](https://github.com/pre-commit/pre-commit-mirror-maker) to sync only `v1.*` semantic release tags from the upstream repository.
