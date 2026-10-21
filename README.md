# B8Launcher distributions

Public installers and update feed for B8 Studios. Application source remains in
[the private B8Launcher repository](https://github.com/ReachX-Labs/B8Launcher).
No Noobsters/ReachX installer or update channel is shared with this repository.

## Build

Organization maintainers run **Build B8 distributions** in
[Noobsters Actions](https://github.com/ReachX-Labs/ReachXLabs/actions/workflows/b8-distribution.yml).
It checks out one immutable B8 commit. This temporary signing broker uses the
existing Apple Developer ID/notarization secrets without exporting them.

Blacksmith builds Windows x64 (NSIS), Linux x64 (AppImage), macOS Apple Silicon
and macOS Intel (DMG plus updater archive). macOS Intel is cross-compiled with
Xcode on a Blacksmith Apple Silicon runner. Updater signatures use B8's own key.

The complete Actions artifact contains installers, signed updater archives,
SHA256SUMS.txt, artifacts.json and latest.json. Aggregation verifies every hash,
platform, version and B8 identity before producing the complete artifact.

## Publication

**No release is published automatically.** No launcher update is authorized by
running the build workflow. A maintainer must separately authorize publication
of the complete verified artifact as a versioned release in this repository.

Future stable feed: `releases/latest/download/latest.json`.
A production app requires the first complete stable release/feed to be published
before distribution to players. Source code, local sessions, server files,
whitelist records and signing private keys must never be uploaded here.