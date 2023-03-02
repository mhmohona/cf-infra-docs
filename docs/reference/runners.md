# Runners

This list is a best effort to compile publicly available information about the runners powering the build infrastructure in conda-forge.
It might not be up-to-date, so in case of doubt refer to the documentation of the provider.

|                         Provider                          |                         Platforms                          | CPU | GPU | RAM  |   Disk    | Time  | Concurrent jobs |                    Notes                     |
| :-------------------------------------------------------: | :--------------------------------------------------------: | :-: | :-: | :--: | :-------: | :---: | :-------------: | :------------------------------------------: |
| [Azure Pipelines][azure] ([Microsoft-hosted][ms-hosted])  | `linux-64`, `win-64`, `linux-aarch64`※‡, `linux-ppc64le`※‡ |  2  | No  | 7GB  | 14GB SSD˟ |  6h   |       100       |          [More details][ms-hosted]           |
|                             ↳                             |                   `osx-64`, `osx-arm64`‡                   |  3  |     | 14GB |           |       |                 |
| [Github Actions][gh-actions] ([Github-hosted][gh-hosted]) | `linux-64`, `win-64`, `linux-aarch64`※‡, `linux-ppc64le`※‡ |  2  | No  | 7GB  | 14GB SSD˟ |  6h   |       100       | Reserved for internal conda-forge usage only |
|                             ↳                             |                   `osx-64`, `osx-arm64`‡                   |  3  |     | 14GB |           |       |                 |
|                    [Travis CI][travis]                    |              `linux-aarch64`, `linux-ppc64le`              |  2  | No  | ~4GB |   ~18GB   | 50min |        ?        |

_※_ Emulated (5-6x performance penalty) <br />
_‡_ Cross-compiled (cannot test) <br />
_˟_ 10GB guaranteed free <br/>

:::info See also
Check the [reference documentation for continuous integration services](./infrastructure/services.md#continuous-integration) for more details.
:::

[azure]: https://azure.microsoft.com/en-us/products/devops/pipelines/
[gh-actions]: https://github.com/features/actions
[ms-hosted]: https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/hosted?view=azure-devops&tabs=yaml
[gh-hosted]: https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners#supported-runners-and-hardware-resources
[travis]: https://travis-ci.com/
