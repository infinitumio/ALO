# Releases

Public builds are published in this repository's [Releases](https://github.com/infinitumio/ALO/releases). They download without a GitHub account.

## Assets

```text
ALO-x.y.z-macos-universal.dmg
ALO-x.y.z-macos-arm64.dmg
ALO-x.y.z-macos-x64.dmg
ALO-x.y.z-windows-x64.exe
ALO-x.y.z-linux-x86_64.AppImage
SHA256SUMS.txt
```

A release only lists the platforms that are ready. Today that is macOS; Windows and Linux will follow.

## Install on macOS

macOS 13 or later.

1. Download the `.dmg`. Universal works on Apple silicon and Intel.
2. Open it.
3. Drag ALO into Applications.
4. Launch ALO.

## Versioning

Semantic versioning. `0.x.y` during early development, `1.0.0` when ALO is stable. Tags look like `v0.4.0`.

## macOS signing

A macOS build is published only after it has been:

1. built in release mode
2. signed with Developer ID, with Hardened Runtime and a secure timestamp
3. notarised by Apple
4. stapled, so the ticket travels with the app and the disk image
5. checked by Gatekeeper on a copy marked as downloaded

If any step fails, nothing is published.

## Verify a download

```sh
shasum -a 256 ALO-0.4.0-macos-universal.dmg
```

Compare the result with the matching line in `SHA256SUMS.txt`. On macOS you can also check the signature:

```sh
spctl --assess --type open --context context:primary-signature -v ALO-0.4.0-macos-universal.dmg
```

## Release notes

Every release uses the same short format:

```md
# ALO 0.4.0

## New
- …

## Improved
- …

## Fixed
- …

## Downloads
See assets below. macOS builds are signed with Developer ID and notarised by Apple.
```
