# FoS IPTV

FoS IPTV v0.1.0 is currently an unsigned macOS test build.

This release is for early testers only. macOS may show a warning such as:

"FoS IPTV" is damaged and can't be opened. You should move it to the Trash.

That warning usually happens because this early build is not Apple Developer ID signed or notarized yet.

FoS IPTV does not include channels, movies, TV shows, playlists, subscriptions, provider access, usernames, passwords, or IPTV credentials.

You must provide your own legal IPTV source.

## Download and install

1. Go to the Releases page.
2. Download FoS-IPTV-v0.1.0-mac-arm64.zip.
3. Unzip it.
4. Try opening FoS IPTV.app.

## macOS unsigned test build fix

If macOS says the app is damaged, run this in Terminal after unzipping the app:

xattr -dr com.apple.quarantine "$HOME/Downloads/FoS IPTV.app"
open "$HOME/Downloads/FoS IPTV.app"

If you moved the app to Applications, run:

xattr -dr com.apple.quarantine "/Applications/FoS IPTV.app"
open "/Applications/FoS IPTV.app"

## Apple Silicon only

The current v0.1.0 release asset is for Apple Silicon Macs only.

Supported:

- M1
- M2
- M3
- M4

Not supported by this asset:

- Intel Macs

To check your Mac type, run:

uname -m

Expected result for this release:

arm64

## Features

- Xtream login with one or more server/base URLs
- Live TV
- Movies / VOD
- TV series and episodes
- M3U playlist import
- XMLTV EPG guide import
- Language and category filtering
- Search across live TV, movies, and series
- Favorites
- Continue watching for movies and episodes
- Multi-server diagnostics
- HTTP 884 provider/block diagnostics
- Local-first storage
- Credential masking

## Important legal notice

FoS IPTV is only a player.

FoS IPTV does not provide IPTV service, channels, movies, series, subscriptions, provider accounts, credentials, playlists, or access to paid content.

You are responsible for making sure you have the legal right to access anything you add to the app.

Do not use FoS IPTV to access pirated, stolen, unauthorized, DRM-protected, geo-blocked, paywalled, device-locked, MAC-locked, or otherwise restricted content.

## License

FoS IPTV v0.1.0 is distributed under the FoS IPTV Free Use License v1.0.

See LICENSE.md.
