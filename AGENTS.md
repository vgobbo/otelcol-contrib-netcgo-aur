# Agent Instructions for otelcol-contrib AUR Package

This repository manages the Arch User Repository (AUR) package for the OpenTelemetry Collector Contrib distribution. It includes custom patches to optimize the collector for ArchLinux environments.

## Repository Overview

- **PKGBUILD**: The primary build script for the package.
- **.SRCINFO**: Generated metadata for the AUR.
- **patches/**: (or root) Contains `.patch` files applied during the build process.
- **config.yaml**: Default configuration for the collector.

## Instructions for LLMs

### 1. Build Process
- Always use `makepkg` to build and verify changes.
- Use `makepkg -o` to only fetch and extract sources if you need to inspect them.
- Use `makepkg -f` to force a rebuild after modifying the `PKGBUILD` or patches.
- **CRITICAL**: Do NOT install the generated package (e.g., using `pacman -U` or `makepkg -i`). Installation is strictly forbidden in this environment.

### 2. Modifying the Source
- Do **not** modify files in `src/` directly for permanent changes.
- Instead, create or update a `.patch` file and include it in the `source` array of the `PKGBUILD`.
- Apply patches within the `prepare()` function of the `PKGBUILD`.

### 3. Updating Metadata
- After any modification to the `PKGBUILD` (including version bumps or patch additions), regenerate the `.SRCINFO` file:
  ```bash
  makepkg --printsrcinfo > .SRCINFO
  ```

### 4. Dependency Management
- Ensure `makedepends` and `depends` in the `PKGBUILD` are accurate.
- If enabling features that require CGO (like the system resolver), ensure `go` and appropriate C libraries are available.

### 5. Version Updates
- When updating the package to a new version:
  1. Update `pkgver` in `PKGBUILD`.
  2. Reset `pkgrel` to `1`.
  3. Run `makepkg -o` to fetch the new source.
  4. Verify if existing patches still apply:
     ```bash
     cd src/opentelemetry-collector-contrib-<version>
     patch --dry-run -p1 -i ../../enable-cgo-netcgo.patch
     ```
  5. If a patch fails, regenerate it.
  6. Update checksums: `updpkgsums`.
  7. Verify the build and update `.SRCINFO`.

### 6. Commit Standards
- Follow [Conventional Commits 1.0](https://www.conventionalcommits.org/en/v1.0.0/).
- Common types: `feat`, `fix`, `chore`, `build`.
