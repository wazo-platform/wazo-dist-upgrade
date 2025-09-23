# wazo-dist-upgrade

Debian distribution utility for Wazo

## Update Procedure

- This package must be backported into:

  - stretch (wazo-dev-stretch + rc + phoenix-stretch & pelican-stretch)
  - buster (wazo-dev-buster + rc + pelican-buster)
  - bullseye (wazo-dev-bullseye + rc + pelican-buster)

  The Jenkins job takes care of `wazo-dev-stretch`, `wazo-dev-buster`,
  `wazo-dev-bullseye` and `wazo-rc`.

  The RC and production distribution must be updated manually.

  Reason: the `wazo-dist-upgrade` package must not change version when running
  `wazo-dist-upgrade`, because the running dist-upgrade script will be replaced.

- `/usr/bin/wazo-dist-upgrade` must be Python/Bash compatible with Stretch,
  Buster, Bullseye and Bookworm

## Content

High-level scripts installed with the package

- `wazo-dist-upgrade`: Wrapper that runs the upgrade script depending on the
  Debian version
- `wazo-dist-upgrade-<debian>`: Upgrade procedure for a specific Debian release
- `wazo-dist-upgrade-<debian>-check`: Runs pre-upgrade checks (Wazo, Debian,
  etc.)

Detailed architecture of `wazo-dist-upgrade-<debian>` (since Debian Bullseye)

- `wazo-dist-upgrade-<debian>`: Symlink providing alternative upgrade paths
  depending on the Wazo edition
- `wazo-dist-upgrade-<debian>-ce`: Community Edition wrapper
- `wazo-dist-upgrade-<debian>-base`: Debian-specific upgrade procedure
