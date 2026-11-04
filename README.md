# bkenks Home Assistant Apps

Home Assistant apps maintained by Brian Kenkel.

## Installation

Add this repository to Home Assistant:

[![Add repository to your Home Assistant instance.][repo-badge]][repo]

Or add it manually: **Settings** > **Apps** > **App store** > menu >
**Repositories**, then enter:

```text
https://github.com/bkenks/home-assistant-apps
```

## Apps

### [Pangolin Site Connector](./pangolin-site-connector)

![Supports aarch64 Architecture][aarch64-shield]
![Supports amd64 Architecture][amd64-shield]

Connects Home Assistant to a [Pangolin][pangolin] server for safe access
from outside your home network. Runs the [Pangolin CLI][pangolin-cli]
site connector. See the [documentation](./pangolin-site-connector/DOCS.md).

## Development

Tools are managed with [mise][mise]:

```sh
mise install
```

The upstream [Home Assistant Community Apps][hassio-addons] example app is
vendored into `.vendir/` for reference with [vendir][vendir]:

```sh
vendir sync
```

`.vendir/` and `.scratch/` are git-ignored.

## Support

Open an [issue on GitHub][issue].

[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[hassio-addons]: https://github.com/hassio-addons/app-example
[issue]: https://github.com/bkenks/home-assistant-apps/issues
[mise]: https://mise.jdx.dev
[pangolin]: https://github.com/fosrl/pangolin
[pangolin-cli]: https://github.com/fosrl/cli
[repo-badge]: https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg
[repo]: https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fbkenks%2Fhome-assistant-apps
[vendir]: https://carvel.dev/vendir/
