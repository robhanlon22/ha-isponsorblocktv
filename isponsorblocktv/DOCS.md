# Setup

1. Install the app. Home Assistant builds the wrapper locally, which can take a few minutes.
2. Pair the TV using the [upstream setup CLI](https://github.com/dmunozv04/iSponsorBlockTV/wiki/Installation). In the TV's YouTube app, select **Settings → Link with TV code**. Use manual pairing; this wrapper does not use network discovery.
3. Copy the resulting device's `screen_id`, `name`, and optional `offset` into the app's **Devices** option, then start the app. Keep pairing identifiers private.

A YouTube API key is needed only when using the channel whitelist.

## Options

- **Devices:** paired TV identifiers, names, and optional timing offsets in milliseconds.
- **Skip categories:** segment categories to skip; defaults to sponsors.
- **Channel whitelist:** channels excluded from skipping; requires a YouTube Data API key.
- **Skip count tracking:** sends skipped-segment identifiers to SponsorBlock. Disabled by default; keep it off to disable reporting.
- **Mute ads / Skip ads:** control YouTube-served ads. These are generally unnecessary with Premium.
- **Auto play:** controls YouTube's automatic playback of the next video.
- **Minimum skip length:** shortest segment to skip, in seconds.
- **Join name:** client name shown on the TV.

## Permissions and updates

The app has its own data directory, ordinary container networking, and Docker's standard AppArmor profile. It requests no shared directories, published ports, HA administrator API, Docker socket, or extra host privileges. Keep Protection mode on.

The Dockerfile selects and verifies an upstream release commit. No upstream code or dependencies are patched. Update the wrapper version and reviewed upstream source together when adopting a new release.

Upstream logs include TV pairing identifiers and watched video IDs. Do not share unredacted logs. Disabling skip reporting does not disable SponsorBlock lookups: those send a short video hash prefix, and the server sees the caller's IP address.

The wrapper is licensed under [Apache-2.0](../LICENSE); upstream iSponsorBlockTV is GPL-3.0.
