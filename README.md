# wazo-dist-upgrade

Debian distribution utility for Wazo

## Update procedure

* This package must be backported into:
    * jessie (wazo-rc + phoenix)
    * stretch (wazo-dev-stretch + rc + phoenix-stretch & pelican-stretch)
    * buster (wazo-dev-buster + rc + pelican-buster)

  The Jenkins job takes care of `wazo-rc`, `wazo-dev-stretch` and `wazo-dev-buster`.

  The RC and production distribution must be updated manually.

  Reason: the `wazo-dist-upgrade` package must not change version when running `wazo-dist-upgrade`, because the running dist-upgrade script will be replaced.
* `/usr/bin/wazo-dist-upgrade` must be Python/Bash compatible with Jessie, Stretch and Buster
