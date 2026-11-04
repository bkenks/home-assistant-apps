# Changelog

All notable changes to this app are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this app follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.0] - 2026-11-03

### Added

- Prebuilt images for `aarch64` and `amd64`, published to
  `ghcr.io/bkenks/pangolin-site-connector/{arch}`.
- GitHub release for each version, with notes from this changelog.
- CI for pull requests: app linter, hadolint, shellcheck, yamllint,
  Prettier, zizmor, test builds for both architectures, and a check that
  `version` is bumped when image files change.

### Changed

- Home Assistant now pulls the prebuilt image instead of building the app
  on your device, so installs and updates are faster.
- The Pangolin CLI version is now set in the `Dockerfile`
  (`PANGOLIN_CLI_VERSION`) instead of `build.yaml`.

## [0.1.0] - 2026-11-03

### Added

- Initial release.
- Runs the [Pangolin CLI](https://github.com/fosrl/cli) `0.20.0` as a
  site connector (`pangolin up site`) on `aarch64` and `amd64`.
- `endpoint`, `id` and `secret` options for connecting to a Pangolin
  server. The app refuses to start while any of them is missing or the
  endpoint is still the example URL.
- `log_level` option, mapped to the site connector's log levels.
- The site connector's config file is persisted in
  `/data/site-config.json`.
- The CLI's built-in self-update is disabled. The CLI version is pinned
  per app release.

[0.2.0]: https://github.com/bkenks/home-assistant-apps/releases/tag/pangolin-site-connector-0.2.0
[0.1.0]: https://github.com/bkenks/home-assistant-apps/releases/tag/pangolin-site-connector-0.1.0
