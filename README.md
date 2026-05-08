# lint

Reusable composite GitHub Action that runs MegaLinter with dynamic flavor detection and optional auto-fix PR creation.

## Usage

```yaml
jobs:
  lint:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      issues: write
      pull-requests: write
      security-events: write
    steps:
      - uses: Skitionek/lint@v1
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          # optional
          # pat: ${{ secrets.PAT }}
```

## Inputs

- `github-token` (optional): token used for checkout, MegaLinter integrations, and fix PR creation fallback.
- `pat` (optional): PAT used by `create-pull-request` so downstream workflows can run.
- `create-fix-pr` (optional, default `true`): whether fix PR creation is enabled.
- `skip-fix-commit-substring` (optional, default `skip fix`): disables fix PR creation when matched in head commit message.

## Outputs

- `has_updated_sources`: `1` when MegaLinter changed tracked files, otherwise `0`.
- `fix_pull_request_url`: URL of the auto-fix PR when created.
- `detected_flavor`: detected MegaLinter flavor (`python`, `javascript`, ..., or `all`).
