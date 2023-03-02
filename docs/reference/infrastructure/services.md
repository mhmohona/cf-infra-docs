# Services & providers

## Github resources

In addition to the thousands of repositories, conda-forge uses several other Github services.

### Organizations

- [`conda-forge`](https://github.com/conda-forge): the main organization
- [`regro`](https://github.com/regro): hosts the `autotick-bot` machinery
- [`channel-mirrors`](https://github.com/channel-mirrors): OCI mirror of the conda-forge channel

:::info
These organizations exist but they are not in active use anymore:

- [`conda-forge-abandoned`](https://github.com/conda-forge-abandoned)
- [`conda-forge-woodpecker-admins`](https://github.com/conda-forge-woodpecker-admins)

:::

### Teams

The `conda-forge` Github organization has thousands of teams.
Most of them are associated to a feedstock, but there a few special ones that are not!

- [`Core`](https://github.com/orgs/conda-forge/teams/Core)
- [`staged-recipes`](https://github.com/orgs/conda-forge/teams/staged-recipes)
- [`help-c-cpp`](https://github.com/orgs/conda-forge/teams/help-c-cpp)
- [`help-cdts`](https://github.com/orgs/conda-forge/teams/help-cdts)
- [`help-go`](https://github.com/orgs/conda-forge/teams/help-go)
- [`help-java`](https://github.com/orgs/conda-forge/teams/help-java)
- [`help-julia`](https://github.com/orgs/conda-forge/teams/help-julia)
- [`help-nodejs`](https://github.com/orgs/conda-forge/teams/help-nodejs)
- [`help-osx-arm64`](https://github.com/orgs/conda-forge/teams/help-osx-arm64)
- [`help-perl`](https://github.com/orgs/conda-forge/teams/help-perl)
- [`help-ppc64le`](https://github.com/orgs/conda-forge/teams/help-ppc64le)
- [`help-pypy`](https://github.com/orgs/conda-forge/teams/help-pypy)
- [`help-python`](https://github.com/orgs/conda-forge/teams/help-python)
- [`help-python-c`](https://github.com/orgs/conda-forge/teams/help-python-c)
- [`help-r`](https://github.com/orgs/conda-forge/teams/help-r)
- [`help-ruby`](https://github.com/orgs/conda-forge/teams/help-ruby)
- [`miniforge`](https://github.com/orgs/conda-forge/teams/miniforge)
- [`all-members`](https://github.com/orgs/conda-forge/teams/all-members)

### Configuration

- [`conda-forge/.github`](https://github.com/conda-forge/.github): Organization-wide configuration, profile information, etc.

### Bot accounts

- [`conda-forge-admin`](https://github.com/conda-forge-admin)
- [`conda-forge-bot`](https://github.com/conda-forge-bot)
- [`conda-forge-coordinator`](https://github.com/conda-forge-coordinator)
- [`conda-forge-daemon`](https://github.com/conda-forge-daemon)
- [`conda-forge-linter`](https://github.com/conda-forge-linter)
- [`conda-forge-manager`](https://github.com/conda-forge-manager)
- [`conda-forge-status`](https://github.com/conda-forge-status)
- [`regro-cf-autotick-bot`](https://github.com/regro-cf-autotick-bot)

:::info
These accounts also exist but are not in active usage anymore:

- [`conda-forge-drone-ci`](https://github.com/conda-forge-drone-ci)

:::

### Apps

- `conda-forge-curator`
- `conda-forge-webservices`

:::info
These apps also exist but are not in active usage anymore:

- `conda-forge drone instance`

:::

### Workflows

- [`beckermr/turnstyle-python`](https://github.com/beckermr/turnstyle-python): Prevents multiple CI jobs from running in parallel to avoid race conditions.
- [`conda-forge/automerge-action`](https://github.com/conda-forge/automerge-action)
- [`conda-forge/github-app-token`](https://github.com/conda-forge/github-app-token) (fork)
- [`conda-forge/webservices-dispatch-action`](https://github.com/conda-forge/webservices-dispatch-action)

## Continuous integration

:::tip See also
Refer to the [`conda-forge.yml` documentation](/docs/reference/feedstock-settings.md#conda-forge-yml) to learn how to configure your CI providers.
:::

### Azure Pipelines

- 🌐 https://dev.azure.com/conda-forge/feedstock-builds/_build
- 📍 Available on all feedstocks
- 🛠 Provides [Microsoft-hosted runners](https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/hosted?view=azure-devops&tabs=yaml) (x64 Linux, macOS and Windows)
- 🔒 Needs access to Anaconda.org (cf-staging)

conda-forge benefits from the generously offered Microsoft-hosted runners.

### Travis CI

- 🌐 https://app.travis-ci.com/github/conda-forge
- 📍 Available on all feedstocks
- 🛠 Provides [native Linux aarch64 and ppc64le runners](https://docs.travis-ci.com/user/reference/overview/)
- 🔒 Needs access to Anaconda.org (cf-staging)

### Cirun

- 🌐 https://cirun.io
- 📍 Available on selected feedstocks only
- 🛠 Provides several architectures (depends on feedstock configuration)
- 🔒 Needs access to Anaconda.org (cf-staging) and the configured backend

Configured with `@conda-forge-daemon`.

Organization-wide configuration can be found in the [`.cirun` repository](https://github.com/conda-forge/.cirun).

### Github Actions

- 🌐 https://github.com/features/actions
- 📍 Not available in feedstocks (only admin tasks)
- 🛠 Provides [GitHub-hosted runners](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners) (x64 Linux, macOS and Windows)
- 🔒 Has access to Github API

### Retired services

- [AppVeyor](https://ci.appveyor.com/account/conda-forge/projects)
- Circle CI
- Drone.io

## Delivery and distribution

### Anaconda.org

- 🌐 Channels / organizations: [`cf-staging`](https://anaconda.org/cf-staging/dashboard), [`conda-forge`](https://anaconda.org/conda-forge/dashboard)
- ⛓ Used by [feedstocks](./feedstocks.md)

### Docker Hub

- 🌐 https://hub.docker.com/u/condaforge/
- ⛓ Used by [`conda-forge/docker-images`](./tooling-data.md#docker-images), [`conda-forge/miniforge-images`](https://github.com/conda-forge/miniforge-images)

### Github Packages

- 🌐 https://github.com/orgs/channel-mirrors/packages
- ⛓ Used by [`channel-mirrors/conda-oci-mirror`](https://github.com/channel-mirrors/conda-oci-mirror)

### Github Releases

- 🌐 https://github.com/conda-forge/miniforge/releases
- ⛓ Used by [`conda-forge/miniforge`](https://github.com/conda-forge/miniforge)

### Quay

- 🌐 https://quay.io/organization/condaforge
- ⛓ Used by [`conda-forge/docker-images`](./tooling-data.md#docker-images)

## Servers

### Heroku

- 🌐 https://hub.docker.com/u/condaforge/
- ⛓ Used by [`webservices`](./automated-maintenance.md#webservices)

## Other services

- Google: `condaforge@gmail.com`
- Google Groups: [conda-forge](https://groups.google.com/g/conda-forge) (retired)
- HackMD: [conda-forge](https://hackmd.io/team/conda-forge)
- Open Collective: [conda-forge](https://opencollective.com/conda-forge/)
- Namecheap (conda-forge.org)
- Twitter: [@condaforge](https://twitter.com/condaforge)
- YouTube: [Conda Forge](https://www.youtube.com/@condaforge3075)
