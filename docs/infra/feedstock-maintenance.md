---
sidebar_position: 2
---

# Feedstock maintenance

Outside the package life cycle, there are some maintenance tasks that conda-forge has to perform every now and then.
All of these are automated, but some of them need to be manually requested and approved by `conda-forge/core`.

Some of these processes need to happen in an order dictated by the conda-forge dependencies graph,
while others can happen in any order.

Graph-depending changes:

- Propagation of a change in the conda-forge pinnings
- Support a new architecture

Non graph-depending changes:

- Source version updates
- Maintenance tasks (refresh credentials, infrastructure updates, ...)

:::info

"Rerendering" is the action of regenerating the supporting workflows, scripts and metadata that you find in every feedstock, next to the `recipe/` directory.
This action is done by `conda-smithy rerender`, which takes `recipe/meta.yaml`, `recipe/conda_build_config.yaml` and `conda-forge.yml` to produce the rest of the content you see in your feedstock.

That content is fed by two main sources:

- The templates defined in `conda-smithy` itself
- The conda-forge pinnings file defined in `conda-forge/conda-forge-pinnings-feedstock`

Anytime there's a change in either, all feedstocks are encouraged to rerender. However, most of the time the new configuration is only needed for the next build of the package. As a result, you can consider that rerenders are lazily delayed until they are needed. It's more efficient and CI-resources-friendly!

However, there are some exceptions, as discussed in this section.
:::

## Graph depending migrations

These changes cannot be applied to all the feedstocks in conda-forge in any random order because their success depends on the availability of packages produced by feedstocks that have already been updated. In other words, the changes need to be done in the order dictated by the conda-forge graph.

The conda-forge graph lists each feedstock _output_ as a node, and nodes connected by the outputs dependencies on each other (e.g. to migrate packages A, B and C, with A depending on B to run and/or be built, the bot would first migrate packages B and C, and A would only get the migration once B has been fully migrated). This is done through automated PRs that contain the migration file and the result of rerendering the feedstock. It's up to the feedstock maintainers to review and merge those PRs, since sometimes the PR introduces changes that do not pass the CI immediately (e.g. updating the pinned version of `openssl` to its newest release, which introduced API incompatible changes that break our package tests). Once merged, that feedstock has successfully completed its part of the migration and the bot can issue the PRs for the dependent feedstocks.

Once the graph is (mostly) migrated, the migration process is "closed", which means that the global file now contains the results of the migration file.

Where are all these pieces of infrastructure defined?

The bot network is built with:

- `regro/cf-scripts`: the logic encoding how to apply the changes driven by the migration scheme
- `regro/autotick-bot`: the CI workflows running the migration logic

The graph metadata is fed by:

- `regro/libcfgraph`, as computed by `regro/libcflib`
- `regro/cf-graph-countyfair`

The progress reports are displayed in:

- [conda-forge.org/status](https://conda-forge.org/status), which is rendered by `conda-forge/status`.
- The data thereby displayed comes from `regro/cf-graph-countyfair`.

The most popular graph-dependent migrations are:

- A change in the conda-forge pinnings
- New architectures added

### Pinnings migrations

<!-- TODO: Put this in the maintainer's guide and link to it in the list above -->

The conda-forge pinnings file is the single source of truth for ABI stability for all conda-forge. Every feedstock contains the subset of that pinnings file that the recipe requires (thanks to `conda-smithy rerender`, which drops platform-specific configurations in the `.ci_support/` directory). With thousands of feedstocks, it wouldn't make sense to rerender all of them just because one definition in that pinnings file has changed. A definition that might not have any impact in that feedstock.

This is why conda-forge uses a special bot to issue those rerender requests through the subset of the feedstock graph that need that "upgrade". The change is not applied to the global file from the beginning; instead, a _migration file_ is created, which contains the operations that would transform the global file into a fully migrated one. When `conda-smithy rerender` finds a migration file under `.ci_support/migrations`, it applies those operations to the global pinnings file, thus migrating that feedstock! Note that several migration files can coexist in the same feedstock at a given time.

<!-- WIP -->

### Support new architectures

Adding support for new architectures is done via the [`arch` migrator](https://github.com/regro/cf-scripts/blob/master/conda_forge_tick/migrators/arch.py), which uses a slightly different mechanism to be triggered, but it's still the `regro/cf-scripts` machinery.

For example, this migrator can add support for:

- `ppc64le`
- `aarch64`
- `osx-arm64`

### Other migrations

Check [`regro/cf-scripts/conda_forge_tick/migrators`](https://github.com/regro/cf-scripts/tree/master/conda_forge_tick/migrators) for all the migration plugins available.
Usage documentation can be found at https://regro.github.io/cf-scripts/.

## Other tasks done while traversing the graph

If an automated task involves submitting a PR for user supervision, it will probably end up in the regro machinery as well. It might not strictly depend on the availability of other packages, but it makes sense to hop on the graph traversal wagon and reuse the same utilities to submit the suggested changes for review.

These tasks involve:

- Updating upstream sources
- Auditing dependencies

When new upstream versions are available, the regro bot will detect it its next cycle and submit a PR to the feedstock.

### Updating upstream sources

The general logic is defined in [this module](https://github.com/regro/cf-scripts/blob/master/conda_forge_tick/update_upstream_versions.py), which will be triggered if the classes defined in [this other module](https://github.com/regro/cf-scripts/blob/master/conda_forge_tick/update_sources.py) detect a new version.

If your feedstock is not receiving updates, it might be because the regro bot cannot "see" it. Consider adding a class to detect them!

:::note
The regro bot will stop submitting "new version available" PRs if the previous **three** PRs have not been merged.

<!--  TODO: Find source code for this check -->

:::

## Automated maintenance

Most of these tasks are taken care by `conda-forge/admin-migrations`.

<!-- TODO: Elaborate -->

### Maintenance rerenders

Each feedstock is equipped with a Github Actions worfklow file defined by the `conda-smithy` templates. The `.github/workflows/webservices.yml` workflow is configured to be triggered on `repository_dispatch` events. It contains an instance of the `conda-forge/webservices-dispatch-action` Github Actions action, which defines several tasks, including:

- Rerendering the feedstock without human intervention

When needed, the conda-forge webservices bot can issue a rerender by triggering that workflow via the required payload. This can be requested by core members in... <!-- FIXME: How? -->

## Manual maintenance

These happen via `conda-forge/admin-requests`.

### Archive a feedstock

Feedstocks may no longer be required for a number of reasons (mostly, being superseded by another one). In these cases, maintainers can request the feedstock be archived. This is also requested via PRs to `conda-forge/admin-requests` and handled by its Github Actions workflows.

This time, only Github access is needed.

### Regenerate tokens

Each feedstock has access to a series of external services, most of them requiring authentication.
Tokens are granted during the feedstock creation process, via `conda-smithy`.
However, sometimes this process can fail or tokens might expire.

In `conda-forge/admin-requests`, maintainers can request that the tokens of a feedstock are regenerated.

This task is also done via the same workflow, but in this case it requires several authentication tokens so `conda-smithy` can issue the required requests. Namely:

- Uploads to Anaconda.org/cf-staging
- CI Services: Azure, Travis, Circle, Drone
- Github: Write access is also needed so the worfklow can commit the changes to the repository
