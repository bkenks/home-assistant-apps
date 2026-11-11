# RELEASE

New releases are triggered by updating an app's version in it's `config.yaml` then pushing/merging into main on GitHub. This means main should always represent a version of the application and work in progress should be on a branch.

Here is the full workflow of creating a new release for a given app:

1. Add an entry in `CHANGELOG.md`.
2. Update the version in `config.yaml`.
3. Create/Push a PR
4. Merge PR -> release triggered