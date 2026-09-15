## 1.0.2

- Add a `pairing_mode` option. On a fresh install the HomeKit data-stream
  recovery always fires 25s after boot (there is no data stream until an Apple
  TV is paired as a target), and it recovers by unpublishing and re-publishing
  the accessory -- which lands mid-pairing and fails the Home app with
  OSStatus -6718 (kNotInitializedErr). Pairing mode pushes the boot grace and
  watchdog timers out to an hour so the accessory can actually be added.

## 1.0.1

- Fix: the add-on could not be built by Supervisor. The Dockerfile copied
  `bridge/index.js`, `bridge/package.json`, `LICENSE`, `NOTICE` and
  `appletv_siri_bridge/run.sh` using repo-root-relative paths, but Supervisor
  builds with the add-on folder as the build context, so every one of those
  COPY steps failed with "not found". CI passes because it builds with
  `context: .`. The add-on folder is now self-contained.

# Changelog

## 1.0.0

First release as a Home Assistant add-on. The bridge itself is unchanged from
the container that has been running since the project started — this packages
it so Home Assistant OS and Supervised users can install it without running
their own Docker container.
