# Staged-recipes

This repository is the gateway to conda-forge. This is where users can submit new recipes which, once reviewed and accepted, will generate a new feedstock and team.

- ⚙️ Deployed in [`conda-forge/staged-recipes`](https://github.com/conda-forge/staged-recipes)
- 🔒 Has access to Azure Pipelines, Github Actions, Travis CI, Anaconda.org (cf-staging)
- 🤖 Integrated with [`webservices`](./automated-maintenance.md#webservices)

## Anatomy of staged-recipes

`recipes/` contains one or more _subdirectories_ with user-submitted recipes.
Most cases will only submit one recipe at a time, but if several subdirectories are present, the `build_all.py` script will build them in the right order so dependencies are satisfied.

`.ci_support` once again contains the conda-build YAML configuration files, but in this case (if compared to feedstocks), you will also find some scripts:

- `build_all.py`: Calls conda-build in the right (topographically sorted) order.
- `compute_build_graph.py`: Supports `build_all.py` by providing the job graph with all the submitted recipes.

The YAML files included in `.ci_support` are minimal and not "rendered" like the ones you find in feedstocks. At runtime, conda-build will take these plus the pinnings take from `conda-forge-pinning`. Also note `staged-recipes` only builds for x64. Support for additional architectures can only be done once a feedstock has been provided.

- Linux: `linux64.yaml` plus the CUDA (10.2, 11.0, 11.1 and 11.2) variants.
- macOS: `osx64.yaml`.
- Windows `win64.yaml`.

The directory `.scripts` contains roughly the same shell scripts that would be used in a feedstock for the CI pipelines. However, since `staged-recipes` does not support "rerendering", these are kept in sync manually and it is common to see some differences.

## Workflows

There are two main jobs that run on `staged-recipes`:

- The `conda-build` jobs that run on every PR (and push to `main`), checking whether the recipes build packages correctly. These jobs run on Azure Pipelines, as defined in [`.azure-pipelines/`](https://github.com/conda-forge/staged-recipes/tree/main/.azure-pipelines).
- The [`create_feedstocks` workflow](https://github.com/conda-forge/staged-recipes/blob/main/.github/workflows/create_feedstocks.yml) that runs after each push to `main` (and every 10 minutes).
  This workflow will create the new feedstock repositories on the `conda-forge` organization.
  The core logic is defined in a Python script at
  [`.github/workflows/scripts/create_feedstocks.py`](https://github.com/conda-forge/staged-recipes/blob/main/.github/workflows/scripts/create_feedstocks.py).

Additional workflows help users set up their recipes correctly. They react to events in PRs:

- [`automate-review-labels`](https://github.com/conda-forge/staged-recipes/blob/main/.github/workflows/automate-review-labels.yml): Updates PR labels to streamline reviews and requests for help.
- [`correct_directory`](https://github.com/conda-forge/staged-recipes/blob/main/.github/workflows/correct_directory.yml): Posts a PR comment in `meta.yaml` and friends were not added in a `recipes/` subdirectory.
- [`do_not_edit_example`](https://github.com/conda-forge/staged-recipes/blob/main/.github/workflows/do_not_edit_example.yml): Posts a PR comment if the `recipes/example/` recipe was edited.

External services connect to `staged-recipes` too:

- The `@conda-forge-linter` bot (deployed at [`webservices`](./automated-maintenance.md#webservices)) will lint and provide hints in PRs based on the contents of the recipe.
