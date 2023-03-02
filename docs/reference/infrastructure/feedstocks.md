---
title: Feedstocks
---

# Feedstocks and other package-building repositories

Most packages in conda-forge come from a repository named `<package_name>-feedstock`, but a very small subset comes from specific, non-feedstock, repositories.

## Feedstocks

- ⚙️ Deployed in Github repositories
- 🔒 Has access to Azure Pipelines, Github Actions, Anaconda.org (cf-staging)
- 🔐 Might have access to Travis CI, Cirun via `admin-requests` (WIP)
- 🤖 Integrated with [`admin-migrations`](./automated-maintenance.md#admin-migrations), [`admin-requests`](./automated-maintenance.md#admin-requests), [`autotick-bot`](./automated-maintenance.md#autotick-bot), [`webservices`](./automated-maintenance.md#webservices).

conda-forge has thousands of feedstocks.
Each feedstock hosts a recipe plus the required pipelines, supporting scripts and configuration metadata.

The contents of a feedstock are well specified. Only two locations are user-managed:

- `recipe/`: Contains the conda-build instructions to build packages. It needs, at least, a `meta.yaml` file. This directory is managed by the user. This is where `conda_build_config.yaml` usually goes.
- `conda-forge.yml`: The feedstock configuration file.

:::warning
You should never manually edit files _not_ listed above! Changes will be overridden in the next feedstock rerender.
:::

Combining these two sources with some external components, `conda-smithy` will generate (render) the contents of the feedstock. Many of the directories are named like that because it is what the external service (e.g. Azure) requests. However, there are some `conda-smithy`-unique directories that are worth discussing:

- `.ci_support/`: Contains the rendered `conda_build_config.yaml` files, passed to `conda-build` via the `-m` flag. Each file here corresponds to one job in the CI build matrix.
- `.ci_support/migrations/`: Special YAML files that instruct `conda-smithy` how to update the `.ci_support/*.yaml` files. These migration files are usually put here by the `autotick-bot` infrastructure, and removed once the migration is considered finished.
- `.scripts/`: Common logic and code supporting the steps you can find in the CI pipelines and local debugging tools.
- `build-locally.py`: A Python script to debug recipes in your machine, roughly equivalent to what's done in the CI pipelines.

:::info Learn more (WIP)

- Rerendering a feedstock
- Recommended workflow

:::

## cdt-builds

- ⚙️ Deployed in [Azure Pipelines](https://dev.azure.com/conda-forge/cdt-builds/_build) via [`conda-forge/cdt-builds`](https://github.com/conda-forge/cdt-builds)
- 🔒 Has access to Azure Pipelines, Anaconda.org (cf-staging)

This special repository builds Core Dependency Tree packages for conda-forge (Linux only).
It doesn't use the feedstock automated machinery.
Instead, it has its own Azure Pipelines workflow and a well documented README.

## msys2-recipes

- ⚙️ Deployed manually from [`conda-forge/msys2-recipes`](https://github.com/conda-forge/cdt-builds)

This is a fork of the old community recipes repository at Anaconda, which includes the `msys2` recipes under the [`msys2/`](https://github.com/conda-forge/msys2-recipes/tree/master/msys2) directory.
Note also the supporting scripts in the [`common-scripts/`](https://github.com/conda-forge/msys2-recipes/tree/master/common-scripts) folder.
