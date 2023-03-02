# Automated maintenance

These components perform actions in automated ways, either triggered by a specific event or continuously as part of a loop.

## admin-migrations

- ⚙️ Deployed in [Github Actions via `conda-forge/admin-migrations`](https://github.com/conda-forge/admin-migrations)
- 🤖 Uses [`@conda-forge-curator`](https://github.com/conda-forge-curator)
- 🔒 Has access to Github API, Anaconda.org (conda-forge and cf-staging), Circle, Travis, Azure, Drone

This repository hosts workflows that are running 24/7.
Its job is to procure an automation loop where some maintenance tasks are added.
Its main user is the core team.

## admin-requests

- ⚙️ Deployed in [Github Actions via `conda-forge/admin-requests`](https://github.com/conda-forge/admin-requests)
- 🤖 Uses [`@conda-forge-curator`](https://github.com/conda-forge-curator)
- 🔒 Has access to Github API, Anaconda.org

This repository hosts workflows that mainly run when triggered by an user-initiated action.
This is usually done via a PR that, once approved, it's merged and triggers the requested action (mark a package as broken, archive a feedstock, etc).

## artifact-validation

- ⚙️ Deployed in [Github Actions via `conda-forge/artifact-validation`](https://github.com/conda-forge/artifact-validation)
- ⛓ Needs [`regro/libcfgraph`](https://github.com/regro/libcfgraph)
- 🤖 Uses [`@conda-forge-curator`](https://github.com/conda-forge-curator)
- 🔒 Has access to Github API, Anaconda.org API

The workflows (and code) to scan artifacts uploaded to [anaconda.org/conda-forge](https://anaconda.org/conda-forge).
Its main output comes in form of [issues in `conda-forge/artifact-validation`](https://github.com/conda-forge/artifact-validation/issues)

## autotick-bot

- ⚙️ Deployed in [Github Actions via `regro/autotick-bot`](https://github.com/regro/autotick-bot)
- ⛓ Needs [`regro/cf-scripts`](https://github.com/regro/cf-scripts), [`regro/cf-graph-countyfair`](https://github.com/regro/cf-graph-countyfair), [`conda-forge/conda-forge-pinning-feedstock`](https://github.com/conda-forge/conda-forge-pinning-feedstock)
- 🤖 Uses [`@regro-cf-autotick-bot`](https://github.com/regro-cf-autotick-bot)
- 🔒 Has access to Github API

This is the repository running the `regro-cf-autotick-bot` workflows.
There are several pipelines in place (see [workflows](https://github.com/regro/autotick-bot/tree/master/.github/workflows)).

## webservices

- ⚙️ Deployed in Heroku Dyno (`conda-forge.herokuapp.com`)
- ⛓ Needs [`conda-forge/conda-forge-webservices`](https://github.com/conda-forge/conda-forge-webservices)
- 🤖 Uses [`@conda-forge-webservices`](https://github.com/conda-forge-webservices), [`@conda-forge-admin`](https://github.com/conda-forge-admin), [`@conda-forge-linter`](https://github.com/conda-forge-linter)
- 🔒 Has access to Github API, Anaconda.org (cf-staging and conda-forge), Heroku

This web application powers several services, like:

- the `@conda-forge-admin, please ...` commands
- the `@conda-forge-linter` bot
- the `cf-staging` to `conda-forge` validation (plus copy)
- status monitoring
