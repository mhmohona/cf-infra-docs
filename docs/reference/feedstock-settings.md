# Feedstock settings

When [`conda-smithy`](./infrastructure/tooling-data.md#conda-smithy) rerenders the contents of the feedstock, it takes into account different sources of configuration:

- `conda-forge.yml`
- `recipe/conda_build_config.yaml`
- `recipe/meta.yaml` (only the `skip: true` lines)
- `.ci_support/migrations/*` (added by the autotick bot)

:::caution
Outside `recipe/`, the only file you are supposed to edit is `conda-forge.yml`.
Everything else is automatically managed!
:::

## conda-forge.yml {#conda-forge-yml}

> WIP. Refer to [`conda_smithy.configure_feedstock._load_forge_config()`](https://github.com/search?q=repo%3Aconda-forge%2Fconda-smithy+symbol%3A_load_forge_config&type=code) in the meantime.

## conda_build_config.yaml

This file is normally used by `conda-build`. It defines how to generate the different variants, among other things. Feel free to consult the [conda-build docs for more details](https://docs.conda.io/projects/conda-build/en/latest/resources/variants.html). On conda-forge, we only need to know about these entries:

```yaml
# TODO WIP
```

## Migration files

```yaml
# TODO WIP
```
