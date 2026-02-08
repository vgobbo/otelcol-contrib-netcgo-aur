# otelcol-contrib AUR Package

This repository contains the build files for the `otelcol-contrib` package, available on the Arch User Repository (AUR). It provides the **OpenTelemetry Collector Contrib** distribution, optimized for Arch Linux.

## Features

- **System Resolver Integration**: Unlike the default upstream builds which are statically linked and use the Go internal resolver, this package is built with `CGO_ENABLED=1` and the `netcgo` build tag. This ensures better integration with Arch Linux's networking stack (e.g., `nsswitch.conf`, `systemd-resolved`).
- **Systemd Integration**: Includes a pre-configured systemd service file and configuration directory.
- **Up-to-date**: Tracks the latest releases of the OpenTelemetry Collector Contrib.

## Installation

Since this is an AUR package, you can build it using an AUR helper or manually:

### Manual Build
1. Clone this repository.
2. Run `makepkg -s` to install dependencies and build the package.
3. Install the resulting package: `sudo pacman -U otelcol-contrib-*.pkg.tar.zst`.

## Configuration

The default configuration files are located in `/etc/otelcol-contrib/`:
- `config.yaml`: The main collector configuration.
- `otelcol-contrib.conf`: Environment variables for the systemd service.

## Development and Maintenance

If you are a developer or an LLM agent working on this repository:
- Refer to `AGENTS.md` for specific instructions on patching, version updates, and build constraints.
- Always regenerate `.SRCINFO` after modifying the `PKGBUILD`.

## Acknowledgments

This package is based on the initial work and maintenance by [Roger Coll](https://github.com/rogercoll).

## License

The build files in this repository are licensed under the same license as the upstream project (Apache 2.0).