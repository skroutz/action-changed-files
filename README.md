# Changed Files Action

A simple action that retrieves the list of changed files in a pull request using the GitHub CLI and filters them with inclusion/exclusion regex patterns.

## Inputs

| Name            | Description                                                                       | Required   | Default   |
| --------------- | --------------------------------------------------------------------------------- | ---------- | --------- |
| `include_regex` | File inclusion pattern as regex. Only files matching the regex will be returned.  | false      | (empty)   |
| `exclude_regex` | File exclusion pattern as regex. Files matching the regex will be ignored.        | false      | (empty)   |

## Outputs

| Name                     | Description                                                                        |
| ------------------------ | ---------------------------------------------------------------------------------- |
| `all_changed_files`      | A space-separated list of all added, copied, modified, renamed and removed files.  |
| `new_or_modified_files`  | A space-separated list of all added, copied, modified or renamed files.            |
| `removed_files`          | A space-separated list of all removed files.                                       |

## Example Usage

```yaml
on:
  pull_request:

jobs:
  example:
    runs-on: ubuntu-latest
    steps:

      - name: Get changed files
        id: changed-files
        uses: skroutz/action-changed-files@v2
        with:
          include_regex: .*\.js

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
