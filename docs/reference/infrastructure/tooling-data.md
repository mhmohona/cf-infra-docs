# Tooling & data

These components do not necessarily perform automation actions on their own (e.g. they don't change the state of a feedstock or a package).
Instead, they support other components in conda-forge's infrastructure.

## conda-smithy

- 📜 Source at [`conda-forge/conda-smithy`](https://github.com/conda-forge/conda-smithy)
- 📦 Packaged at [`conda-forge/conda-smithy-feedstock`](https://github.com/conda-forge/conda-smithy-feedstock)
- 📖 [Documentation](https://github.com/conda-forge/conda-smithy/blob/main/README.md)

This is the main feedstock creation and maintenance tool.

Most of its usage is automated by our infrastructure:

- Feedstock creation and services registration at `staged-recipes`
- Regeneration (rerendering), linting and hinting in PRs done by `conda-forge-linter` on `webservices`

However, you can also use it locally or on your forge-like deployments. For local debugging, you will find these commands useful:

- `conda-smithy rerender`
- `conda-smithy recipe-lint`

---

## conda-forge-pinning

- ⚙️ Deployed in [Anaconda.org](https://anaconda.org/conda-forge/conda-forge-pinning) via [`conda-forge/conda-forge-pinning-feedstock`](https://github.com/conda-forge/conda-forge-pinning-feedstock)
- 🔒 Has access to Azure, Anaconda.org (cf-staging)

Hosts the global pinnings for conda-forge, and the ongoing migrations.

## conda-forge-repodata-patches

- ⚙️ Deployed in [Anaconda.org](https://anaconda.org/conda-forge/conda-forge-repodata-patches) via [`conda-forge/conda-forge-repodata-patches`](https://github.com/conda-forge/conda-forge-repodata-patches)
- 🔒 Has access to Azure, Anaconda.org (cf-staging)

This repository creates the `repodata.json` patches used by the Anaconda.org to amend the metadata coming from the published packages.

Read more bout this in [The package life cycle](/docs/fundamentals/life-cycle.md#post-publication-particularities-1).

---

## conda-forge-ci-setup

- ⚙️ Deployed in [Anaconda.org](https://anaconda.org/conda-forge/conda-forge-ci-setup) via [`conda-forge/conda-forge-pinning-feedstock`](https://github.com/conda-forge/conda-forge-ci-setup-feedstock)
- 🔒 Has access to Azure, Anaconda.org (cf-staging)

This special feedstock provides a package that defines the logic to install and configure a common CI setup across providers.

## docker-images

- ⚙️ Deployed in [`conda-forge/docker-images`](https://github.com/conda-forge/docker-images)
- 🔒 Has access to [DockerHub](./services.md#docker-hub) and [Quay.io](./services.md#quay)
- ⛓ Needed by `staged-recipes`, feedstocks.

This repository builds the Docker images used to provide a unified system on all Linux builds.

---

## regro/cf-scripts

- 📜 Source at [`regro/cf-scripts`](https://github.com/regro/cf-scripts)
- 📖 [Documentation](https://regro.github.io/cf-scripts/)

The code and logic behind [`autotick-bot`](./automated-maintenance.md#autotick-bot).

## regro/cf-graph-countyfair

- ⚙️ Deployed in [Github Actions via `regro/cf-graph-countyfair`](https://github.com/regro/cf-graph-countyfair)
- ⛓ Needs [`regro/cf-scripts`](#regrocf-scripts), [`conda-forge/conda-forge-pinning-feedstock`](#conda-forge-pinning)
- 🤖 Uses [`@regro-cf-autotick-bot`](./services.md#bot-accounts)
- 🔒 Has access to Github API

This is the graph data used by [`autotick-bot`](./automated-maintenance.md#autotick-bot).
The logic to build the graph is provided by [`cf-scripts`](#regrocf-scripts).

## regro/libcfgraph

- ⚙️ Deployed in [Circle CI](https://app.circleci.com/pipelines/github/regro/libcfgraph) via [`regro/libcfgraph`](https://github.com/regro/libcfgraph)
- ⛓ Needs [`regro/libcflib`](#regrolibcflib)
- 🤖 Commits as `circleci` (fake username)
- 🔒 Has access to Github API, Circle CI

The libcfgraph data is similar to [`cf-graph-countyfair`](#regrocf-graph-countyfair).

<!-- TODO: Explain differences in form and purpose -->

## regro/libcflib

- 📜 Source at [`regro/libcflib`](https://github.com/regro/libcflib)
- 📦 Packaged at [`conda-forge/libcflib-feedstock`](https://github.com/conda-forge/libcflib-feedstock)
- 📖 Not documented

This is the code that builds the data served at [`libcfgraph`](#regrolibcfgraph).

## feedstocks monorepo

- ⚙️ Deployed in [`conda-forge/feedstocks`](https://github.com/conda-forge/feedstocks)

A single repository containing all feedstocks as submodules.

## feedstock-outputs

- ⚙️ Deployed in [Github Actions via `conda-forge/feedstock-outputs`](https://github.com/conda-forge/feedstock-outputs)
- 🔒 Has access to Azure, Anaconda.org (cf-staging)

This repository is a registry of feedstock names and the packages (artifacts) they produce.
Its main purpose is to provide an allow-list for the validation server to prevent malicious cross-feedstock builds, although it's also an informative map of `feedstocks <-> packages` that is exposed in the [packages section of the website](https://conda-forge.org/feedstock-outputs/).

## Others

- [`regro/conda-suggest-conda-forge`](https://github.com/regro/conda-suggest-conda-forge) provides [`conda-suggest`](https://github.com/conda-incubator/conda-suggest) files that map executables to package names.
