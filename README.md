# pylint-action

This action will set up python, install requirements, and then run pylint.
Passing checks are gated by any settings defined in pylint's configuration.
Pull request annotation will automatically be set up by this action.
Arguments may be passed to pylint by supplying a `args` input to the action.

This action will use a `pylintrc` (or `.pylintrc`, `pyproject.toml`, or `setup.cfg`) file in the root directory of the calling repository to configure how pylint runs.
See https://pylint.pycqa.org/en/latest/user_guide/usage/run.html#command-line-options.

This action can be called independently or called via the `open-reading-frame/reusable-workflows/.github/workflows/static-analysis.yml` reusable workflow.

## Example

```yaml
name: pylint

on:
  push:
    branches: [main]  # Or the name of your default branch
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  pylint:
    name: pylint
    runs-on: ubuntu-latest
    steps:
      - name: Run pylint
        uses: open-reading-frame/pylint-action@main
        with:
          python-version: <default 3.10>
          requirements-txt: <path/to/requirements.txt>
          build-command: <optional command to run after installing python dependencies and before pylint>
          pylint-version: <default latest>
          args: <default --recursive=true .>
```
