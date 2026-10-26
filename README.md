# B8Launcher distributions

[Download B8Launcher](https://github.com/ReachX-Labs/B8Launcher-dist/releases/latest)

Installers and signed automatic updates are hosted on the Noobsters CDN in B8's independent namespace:

- Stable feed: <https://cdn.noobsters.net/b8launcher/stable/latest.json>
- Versioned files: `https://cdn.noobsters.net/b8launcher/releases/<version>/<platform>/<filename>`
- Source: [private B8Launcher repository](https://github.com/ReachX-Labs/B8Launcher).

The `latest.json` asset in release 0.0.13 is a compatibility bridge for existing B8Launcher 0.0.11/0.0.12 installations. It downloads 0.0.13 from the CDN. From 0.0.13 onward, the launcher checks the CDN directly. This repository's feed does not need to change for subsequent CDN releases.

## Build and publish

Organization maintainers bump the B8 version, then manually run **Publish signed B8 updates to Noobsters CDN** in [Noobsters Actions](https://github.com/ReachX-Labs/ReachXLabs/actions/workflows/b8-distribution.yml), supplying the full B8 source commit SHA. This workflow **publishes a stable B8 update** after validation.

Blacksmith builds Windows x64 (NSIS), Linux x64 (AppImage), macOS Apple Silicon and Intel (DMG and signed updater archives). Apple credentials remain in the original signing broker; B8 uses its own updater signing key. Intel is cross-compiled and needs a hardware smoke test.

Bundles transfer directly into private CDN staging without GitHub Actions artifacts. Production identity, Bola8Studios scope, source/Core provenance, SHA-256 checksums and actual Tauri updater signatures are verified before the stable feed changes atomically. Failed builds preserve the previous stable feed; published versions are immutable. A final native Tauri probe downloads and validates all four platforms without installing them.

B8's update channel and application identity are independent of the general Noobsters launcher. Source code, player sessions, server files, whitelist records and private signing keys are never published here or in the CDN release folders.
