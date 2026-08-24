# mechanix-flutter-engine

`libflutter_engine.so` and `libflutter_elinux_wayland.so`, packaged and
shared across every Mechanix Flutter/eLinux app.

## What this package installs

Standard system lib locations for the two shared libraries:

- rpm (Fedora): `/usr/lib64/libflutter_engine.so`,
  `/usr/lib64/libflutter_elinux_wayland.so`
- deb (Debian/Ubuntu, aarch64 multiarch): `/usr/lib/aarch64-linux-gnu/libflutter_engine.so`,
  `/usr/lib/aarch64-linux-gnu/libflutter_elinux_wayland.so`

Consuming apps must add
`depends: ["mechanix-flutter-engine = <version>"]` to their
`packaging/nfpm/nfpm.yaml` - an exact version pin, since these libraries
have no ABI-stable so name and mismatched versions can misbehave silently.

## Versioning

The package version is the flutter-elinux tag it was built from (e.g.
`3.47.0`), pinned explicitly in the CI workflow. Bumping the engine version means bumping the pin here, publishing a new package version, and updating every
consuming app's `depends:` pin together - it's a coordinated release.

## Build

CI (`.github/workflows/build-aarch64.yml`) clones the pinned flutter-elinux
tag, runs `flutter-elinux precache --elinux` to fetch the prebuilt engine
artifacts and packages `elinux-arm64-release/{libflutter_engine.so,libflutter_elinux_wayland.so}`
