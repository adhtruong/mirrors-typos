# mirrors-typos

Mirror of [typos](https://github.com/crate-ci/typos) for pre-commit.

## Background

`.pre-commit-config.yaml` is included in repo but uses tagging strategy tags `v1`, semantic release tag and subpackage tag. This does not interact well `pre-commit autoupdate` as `v1` is a mutable tag. This repos mirrors tags filtering by `v1.*` so only semantic release tags are fetched.

See [here](https://github.com/crate-ci/typos/issues/390) for discussion in repo.

## Usage

```yaml
repos:
  - repo: https://github.com/adhtruong/mirrors-typos
    rev: v1.31.0
    hooks:
      - id: typos
```

This can be configured based on usage guide in source repo.

### Differences with typos pre-commit

- Only `typos` from binary is supported.
- Stages not specified. This is not supported by tool to generate this repo.
