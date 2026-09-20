# Uptime Kuma

> TOS 7 application package for **Uptime Kuma** — platform integration only.
> The application itself is provided by the upstream project, unmodified.

## Overview

A self-hosted monitoring tool for tracking service uptime with status pages.

上游项目 / Upstream: <https://github.com/louislam/uptime-kuma>
上游许可证 / License: **MIT**

## Features

- HTTP(s), TCP, Ping, DNS and push monitors
- Certificate expiry monitoring
- Public status pages
- Notifications via 90+ providers

## Installation

1. Requirements: TOS 7.0+ and Docker Engine (install from the TOS App Center)
2. Install from the TOS App Center
3. Open the app and complete initial configuration

## Usage

1. Access URL: `http://${ip}:18803`
2. Default credentials: see upstream documentation
3. Key settings: see upstream documentation

## Permissions

| Permission | Rationale |
|---|---|
| Network: port 18803 | Web UI access |
| File system: `/Volume*/DockerAppData/shh3-uptime-kuma/` | Application data persistence |
| User: shh3uptimekuma | Isolated non-root service execution |

## Configuration

See `config.ini` for platform metadata; see `docker-compose.yml` for runtime configuration.

## Ports

| Port | Protocol | Purpose |
|---|---|---|
| 18803 | TCP | Web UI (Uptime Kuma) |

## Support

- Documentation: https://github.com/louislam/uptime-kuma
- Issue tracker: https://github.com/louislam/uptime-kuma/issues
- Community: https://github.com/louislam/uptime-kuma

## Security & Compliance

- **License**: MIT — full text in [`LICENSE`](./LICENSE)
- **Attribution**: see [`NOTICE`](./NOTICE)
- **Privacy Policy**: see [`PRIVACY.md`](./PRIVACY.md)
- **Vulnerability scan**: `trivy-report.txt` attached to each Release (HIGH/CRITICAL must be 0)
- Runs as a non-root dedicated user; no privileged mode, no host network

## Changelog

### v1.0.1 (2026-09-20)
- Compliance update: added LICENSE / NOTICE / PRIVACY materials,
  declared upstream license inside the package, added container healthcheck

### v1.0.0
- Initial release

## License

**MIT** — this packaging repository is distributed under the same license as the
upstream project. Full text: [`LICENSE`](./LICENSE).
