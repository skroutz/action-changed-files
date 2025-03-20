# Changed Files Action

A simple action that retrieves the list of changed files in a pull request using the GitHub CLI and filters them with inclusion/exclusion regex patterns.

## Inputs

| Name   | Description                                                                                     | Required | Default |
|--------|-------------------------------------------------------------------------------------------------|----------|---------|
| `files`   | File inclusion patterns as regex (one per line). Each line is combined with a pipe   | false    | (empty) |
| `exclude` | File exclusion patterns as regex (one per line). Each line is combined with a pipe   | false    | (empty) |

## Outputs

| Name                   | Description                                                                              |
|------------------------|------------------------------------------------------------------------------------------|
| `all_changed_files`    | A space-separated list of all added, copied, modified, and renamed files.               |
| `all_changed_files_count` | The total number of files in `all_changed_files`.                                     |

## Example Usage

```yaml
on:
  pull_request:

jobs:
  example:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Get changed files
        id: changed-files
        uses: skroutz/action-changed-files@v1
        with:
          files: |
            .*\.js
            .*\.jsx

      - name: Print changed files
        run: |
          echo "All changed files: ${{ steps.changed-files.outputs.all_changed_files }}"
          echo "Number of changed files: ${{ steps.changed-files.outputs.all_changed_files_count }}"
```
## How to release

```bash
git tag v1.1.0   (replace with the needed version)
git push origin v1.1.0 (replace with the needed version)
```
