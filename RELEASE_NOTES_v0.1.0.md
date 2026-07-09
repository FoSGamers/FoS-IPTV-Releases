# FoS IPTV v0.1.0 — unsigned macOS test build

This is the first public test release of FoS IPTV.

Important: this is an unsigned and non-notarized macOS test build. It is meant for early testers before the app has full Apple Developer ID signing and notarization.

## macOS damaged-app warning

macOS may show this warning:

"FoS IPTV" is damaged and can't be opened. You should move it to the Trash.

That usually happens because this early GitHub build is not signed or notarized yet.

After downloading and unzipping the app, run this in Terminal if the app is in Downloads:

xattr -dr com.apple.quarantine "$HOME/Downloads/FoS IPTV.app"
open "$HOME/Downloads/FoS IPTV.app"

If you moved it to Applications, run:

xattr -dr com.apple.quarantine "/Applications/FoS IPTV.app"
open "/Applications/FoS IPTV.app"

## Apple Silicon only

This release asset is for Apple Silicon Macs only.

Supported:

- M1
- M2
- M3
- M4

This asset is not for Intel Macs.

To check your Mac type, run:

uname -m

Expected result:

arm64

## What FoS IPTV is

FoS IPTV is a free desktop IPTV player for users who already have their own legal IPTV playlist or Xtream-compatible provider account.

FoS IPTV does not include channels, movies, series, playlists, provider access, subscriptions, usernames, passwords, or IPTV credentials.

## Add your own Xtream account

1. Open FoS IPTV.
2. Go to Sources.
3. Select Xtream login.
4. Paste your provider base URL or URLs into Server URL(s), one per line.
5. Enter your username.
6. Enter your password.
7. Click Test connection.
8. If the diagnostic passes, click Connect & import.
9. Browse Live TV, Movies, Series, Search, or Guide.

Do not post your real server URL, username, or password publicly.

## Features

- Xtream multi-server login
- Live TV
- Movies / VOD
- TV series and episodes
- M3U playlist import
- XMLTV EPG
- Language/category filtering
- Search across Live TV, Movies, and Series
- Favorites
- Continue watching for Movies and Episodes
- HTTP 884 diagnostics
- Credential masking
- Local-first storage

## Known limitations

- Unsigned macOS test build
- Not notarized yet
- Apple Silicon only for this asset
- Provider support varies
- Some providers block M3U, VOD, or series endpoints
- Language detection is conservative
- FoS IPTV does not include IPTV content or subscriptions
