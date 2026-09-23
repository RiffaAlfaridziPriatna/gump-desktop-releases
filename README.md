# GUMP Desktop Releases

Public feed and binaries for **GUMP Desktop** auto-update ([Sparkle](https://sparkle-project.org/) on macOS, [WinSparkle](https://winsparkle.org/) on Windows).

This repository does **not** contain application source code.

## What lives here

| Path / surface | Purpose |
|----------------|---------|
| [`appcast.xml`](./appcast.xml) on `main` | Sparkle / WinSparkle update feed (clients read the raw URL) |
| [GitHub Releases](../../releases) | Versioned `.zip` artifacts (`Gump-MacOS-v*.zip`, `Gump-Windows-v*.zip`) |

Do **not** commit large zip files into git. Upload them only as Release assets.

## Client feed URL

After the source app is pointed at this repo:

```text
https://raw.githubusercontent.com/RiffaAlfaridziPriatna/gump-desktop-releases/main/appcast.xml
```

Enclosure URLs inside `appcast.xml` must use this repo’s Releases, for example:

```text
https://github.com/RiffaAlfaridziPriatna/gump-desktop-releases/releases/download/<tag>/Gump-MacOS-v<version>.zip
```

## How releases are published

Builds run in the private/source repository (`gump-desktop`). CI then:

1. Creates a GitHub Release **here** for the date tag (e.g. `2026-09-23`)
2. Uploads macOS + Windows zips (and keeps the release **published**, not draft)
3. Updates `appcast.xml` on this repo’s `main`

EdDSA signatures for Sparkle are produced in the source CI (`sign_update`) and written into `appcast.xml`.

## Manual checks

```bash
# Feed reachable
curl -fsSL https://raw.githubusercontent.com/RiffaAlfaridziPriatna/gump-desktop-releases/main/appcast.xml | head

# Zip from appcast must be HTTP 200 (not draft / missing asset)
curl -sI "https://github.com/RiffaAlfaridziPriatna/gump-desktop-releases/releases/download/<tag>/Gump-MacOS-v<version>.zip"
```

## License / ownership

Binaries and update metadata for GUMP Desktop © Gump Ai Limited.  
Source code remains in the separate `gump-desktop` repository.
