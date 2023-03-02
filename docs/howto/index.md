---
sidebar_position: 4
---

# How-to guides

> This page temporarily holds miscellaneous notes while the rest of the documentation is written.

## Pipeline triggers

The feedstock pipelines are set up to react on the following triggers:

- Pushes to `main` and, by default, all other branches in the repository.
  This includes the initial commit for the feedstock creation.
  When triggered this way, the pipelines **will upload** the artifacts produced by successful builds to the validation server.
- Pushes to a PRs targetting any branch.
  These will not result in uploads to any server, even if successful.

:::caution

Do note that since pushes to a branch result in uploads, any PRs you open **must be created from a fork**.
Do NOT create branches in the feedstock to open PRs.

:::

## Recommended workflow

If you want to change how your package is built, the pipelines are set up to encourage the following workflow:

1. Fork the feedstock to your account or organization.
2. Open a new branch off the up-to-date `upstream/main` branch.
3. Add the needed changes to the `recipe/` directory contents.
4. Open the PR against `upstream/main`.
5. Make sure all the CI entries are passing.
6. Merge the PR.
7. Let the pipelines build and upload your artifacts to the validation server.
8. Wait until the artifacts land on `conda-forge` and are synced in the CDN (~30 min).
