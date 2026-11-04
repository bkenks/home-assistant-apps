# Home Assistant App: Pangolin Site Connector

Connects Home Assistant to a [Pangolin][pangolin] server so you can reach
it safely from outside your home network, without opening ports on your
router.

The app runs the [Pangolin CLI][pangolin-cli] as a site connector
(`pangolin up site`). The site connector opens an outbound WireGuard
tunnel to your Pangolin server. Pangolin then proxies requests for your
public domain through that tunnel to Home Assistant.

## Prerequisites

- A running Pangolin server reachable from your Home Assistant host.
- A site created in the Pangolin dashboard. Copy its
  **ID** and **Secret** when you create it; the secret is shown only once.
- A resource in Pangolin that targets your Home Assistant instance
  (for example `http://homeassistant:8123`, Home Assistant's hostname on
  the internal app network).

## Installation

1. Add this repository to Home Assistant:

   [![Add repository to your Home Assistant instance.][repo-badge]][repo]

1. Find the "Pangolin Site Connector" app in the app store and click
   "Install".
1. Open the "Configuration" tab and fill in `endpoint`, `id` and `secret`.
1. Configure Home Assistant to trust the proxy (see below).
1. Start the app.
1. Check the logs for `Configuration is valid.` and a successful tunnel
   connection.

## Configuration

**Note**: _Restart the app after you change the configuration._

Example app configuration:

```yaml
endpoint: "https://pangolin.example.com"
id: "your-site-id"
secret: "your-site-secret"
log_level: info
```

### Option: `endpoint`

The URL of your Pangolin server, for example
`https://pangolin.example.com`. The app refuses to start while this is
still the example URL.

### Option: `id`

The site ID from the Pangolin dashboard.

### Option: `secret`

The site secret from the Pangolin dashboard.

### Option: `log_level`

Controls how much the app logs. Possible values are:

- `trace`: Show every detail, like all called internal functions.
- `debug`: Shows detailed debug information.
- `info`: Normal (usually) interesting events.
- `notice`: Normal but significant events.
- `warning`: Exceptional occurrences that are not errors.
- `error`: Runtime errors that do not require immediate action.
- `fatal`: Something went terribly wrong. App becomes unusable.

Each level includes messages from more severe levels. The default is
`info`.

The site connector has fewer log levels, so the app maps them as follows:

| App level        | Site connector level |
| ---------------- | -------------------- |
| `trace`, `debug` | `DEBUG`              |
| `info`, `notice` | `INFO`               |
| `warning`        | `WARN`               |
| `error`          | `ERROR`              |
| `fatal`          | `FATAL`              |

## Home Assistant proxy setup

Home Assistant rejects proxied requests with `400: Bad Request` until it
trusts the proxy. Since Home Assistant 2026.8, these settings live in the
UI instead of `configuration.yaml`:

1. Go to **Settings** > **System** > **Network**.
1. Expand the **HTTP server** section.
1. Enable **X-Forwarded-For** support.
1. Add `172.30.33.0/24` as a trusted proxy.
1. Save, then restart Home Assistant.

`172.30.33.0/24` is the internal network Home Assistant assigns to apps.

**Note**: _An `http:` block in `configuration.yaml` is no longer applied.
Remove it if you have one, to avoid confusion._

## Data

The site connector stores its state in `/data/site-config.json`. This file
is kept across restarts and included in Home Assistant backups.

The app pins a specific Pangolin CLI version and disables the CLI's
built-in self-update. New CLI versions arrive through app updates.

## Troubleshooting

- **App stops right after start**: Check the log. A missing `endpoint`,
  `id` or `secret`, or the example `endpoint`, stops the app with a
  message saying which one.
- **`400: Bad Request` in the browser**: Complete the proxy setup above.
- **Tunnel does not connect**: Confirm the ID and secret match the site in
  Pangolin. Set `log_level` to `debug` and check the log.

## Changelog & Releases

Releases follow [Semantic Versioning][semver] (`MAJOR.MINOR.PATCH`):

- `MAJOR`: Incompatible or major changes.
- `MINOR`: Backwards-compatible new features and enhancements.
- `PATCH`: Backwards-compatible bugfixes and package updates.

See the [changelog](CHANGELOG.md) for the changes in each release.

## Support

Open an [issue on GitHub][issue].

## Authors & contributors

Maintained by [Brian Kenkel][bkenks]. Built on the
[Home Assistant Community Apps][hassio-addons] example app by Franck
Nijhof.

## License

This app is licensed under the MIT License. The bundled
[Pangolin CLI][pangolin-cli] binary is licensed under AGPL-3.0.

[bkenks]: https://github.com/bkenks
[hassio-addons]: https://github.com/hassio-addons/app-example
[issue]: https://github.com/bkenks/home-assistant-apps/issues
[pangolin]: https://github.com/fosrl/pangolin
[pangolin-cli]: https://github.com/fosrl/cli
[repo-badge]: https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg
[repo]: https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fbkenks%2Fhome-assistant-apps
[semver]: https://semver.org/spec/v2.0.0.html
