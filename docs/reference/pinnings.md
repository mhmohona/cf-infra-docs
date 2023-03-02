---
title: Pinnings
---

<!-- TODO: This could be automated somehow -->

# Global pinnings & configuration

For consistent builds and inter-artifact compatibility, many of the libraries and projects used to build packages on conda-forge are pinned or locked to a globally controlled value. We call this "pinnings". This includes compilers, runtime libraries, base systems, and others.

:::info

This information is collected here for your convenience, but it might not be up-to-date with the authoritative source: `conda-forge-pinnings`.
[Check this file for up-to-date values](https://github.com/conda-forge/conda-forge-pinning-feedstock/blob/main/recipe/conda_build_config.yaml).
:::

## Base systems

### Linux

On Linux, we use a combination of CentOS-based Docker images with a matching sysroot package to target an old enough `glibc` version:

| Platform        | `glibc` | Base image | Sysroot |
| :-------------- | :-----: | :--------: | :-----: |
| `linux-64`      |  2.12   |  CentOS 7  |  2.12   |
| `linux-aarch64` |  2.17   |  CentOS 7  |  2.17   |
| `linux-ppc64le` |  2.17   |  CentOS 7  |  2.17   |

### macOS

On macOS, we pin to an old enough `MACOS_DEPLOYMENT_TARGET` value:

| Platform    | `MACOSX_DEPLOYMENT_TARGET` |       `macos_machine`       |
| :---------- | :------------------------: | :-------------------------: |
| `osx-64`    |            10.9            | `x86_64-apple-darwin13.4.0` |
| `osx-arm64` |            11.0            | `arm64-apple-darwin20.0.0`  |

### Windows

On Windows, we rely on the version of `ucrt`, `vc` and other redistributable libraries:

| Platform | `ucrt` | `vc` |
| :------- | :----: | :--: |
| `win-64` |  10.9  |      |

## C & C++ {#c}

| Platform        |      Compiler      |
| :-------------- | :----------------: |
| `linux-64`      |       GCC 11       |
| `linux-aarch64` |       GCC 11       |
| `linux-ppc64le` |       GCC 11       |
| `osx-64`        |      clang 14      |
| `osx-arm64`‡    |      clang 14      |
| `win-64`        | Visual Studio 2019 |

_‡_ Cross-compiled only <br />

## CUDA

| Platform         | `nvcc` |  C, C++, Fortran   | `cudnn` | `glibc` |
| :--------------- | :----: | :----------------: | :-----: | :-----: |
| `linux-64`       |  10.2  |       GCC 7        |    7    |  2.12   |
| `linux-64`       |  11.0  |       GCC 9        |    8    |  2.17   |
| `linux-64`       |  11.1  |       GCC 10       |    8    |  2.17   |
| `linux-64`       | 11.2+  |       GCC 10       |    8    |  2.17   |
| `linux-aarch64`‡ |  11.2  |       GCC 10       |    8    |  2.17   |
| `win-64`         |  10.2  | Visual Studio 2019 |    7    |   --    |
| `win-64`         |  11.0  | Visual Studio 2019 |    8    |   --    |
| `win-64`         |  11.1  | Visual Studio 2019 |    8    |   --    |
| `win-64`         | 11.2+  | Visual Studio 2019 |    8    |   --    |

_‡_ Cross-compiled only <br />

## Fortran

| Platform  |  Compiler   |
| :-------- | :---------: |
| `linux-*` | GFortran 11 |
| `osx-64`  | GFortran 11 |
| `win-64`  |   Flang 5   |

## Go

|    `go-nocgo`    |     `go-cgo`     |
| :--------------: | :--------------: |
| Latest available | Latest available |

## Node.js

| Platform     |  `nodejs`  |
| :----------- | :--------: |
| `linux-*`    | 14, 16, 18 |
| `osx-64`     | 14, 16, 18 |
| `osx-arm64`‡ |   16, 18   |
| `win-64`     | 14, 16, 18 |

_‡_ Cross-compiled only <br />

## Perl

| `perl` |
| :----: |
| 5.32.1 |

## Python

| Python implementation | Python version | NumPy version |
| :-------------------: | :------------: | :-----------: |
|        CPython        |      3.8       |     1.20      |
|        CPython        |      3.9       |     1.20      |
|        CPython        |      3.10      |     1.21      |
|        CPython        |     3.11※      |     1.23      |
|         PyPy          |      3.8※      |     1.20      |
|         PyPy          |      3.9※      |     1.20      |

_※_ Only via migration

## R

| Platform  | `r_base` |
| :-------- | :------: |
| `linux-*` | 4.1, 4.2 |
| `osx-*`   | 4.1, 4.2 |
| `win-64`  |   4.1    |

## Rust

|      `rust`      |
| :--------------: |
| Latest available |

---

:::info
Check [`conda-forge-pinnings`](https://github.com/conda-forge/conda-forge-pinning-feedstock/blob/main/recipe/conda_build_config.yaml) for more details.
:::
