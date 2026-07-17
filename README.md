# FoS IPTV

**FoS IPTV v0.2.0** is the current public release — a free desktop
IPTV player for people who already have their own legal IPTV sources.

This is an **unsigned public test build**. It is not Apple Developer ID signed
and not notarized yet, it is for **Apple Silicon** Macs only (mac-arm64), and
it is meant for early testers.

FoS IPTV does not include, sell, discover, recommend, or provide television channels, movies, series, playlists, subscriptions, or provider accounts.
You bring your own legal M3U/M3U8 playlists, Xtream-compatible accounts and
XMLTV guides, and you are responsible for having the legal right to use them.

## Download and install

1. Open the [Releases page](https://github.com/FoSGamers/FoS-IPTV-Releases/releases)
   and pick **v0.2.0**.
2. Download one of the two packages (both are the same app):
   - `FoS-IPTV-0.2.0-mac-arm64.dmg` — open it and drag **FoS IPTV**
     into **Applications** (recommended).
   - `FoS-IPTV-0.2.0-mac-arm64.zip` — unzip it and move
     **FoS IPTV.app** into **Applications**.
3. Because the build is unsigned, clear the quarantine flag once before the
   first launch (next section).

Each release lists the exact SHA-256 checksum and byte size of every package
in its release notes and update manifest, so a download can be verified before
it is opened.

## macOS "damaged app" warning (unsigned build)

macOS may show:

> "FoS IPTV" is damaged and can't be opened. You should move it to the Trash.

That happens because this build is not signed or notarized yet — Gatekeeper
quarantines downloaded, unsigned apps. It does not mean the download is
broken. Clear the quarantine attribute once in Terminal.

If the app is still in Downloads:

```bash
xattr -dr com.apple.quarantine "$HOME/Downloads/FoS IPTV.app"
open "$HOME/Downloads/FoS IPTV.app"
```

If you moved it to Applications:

```bash
xattr -dr com.apple.quarantine "/Applications/FoS IPTV.app"
open "/Applications/FoS IPTV.app"
```

## Apple Silicon only

This release runs on Apple Silicon Macs only (M1/M2/M3/M4). There is no
Windows, Linux or Intel-Mac package in this release — other platforms are
published only after they are validated on real hardware. To check your Mac,
run `uname -m` in Terminal; the expected result is `arm64`.

## Features

- Live TV from your own M3U/M3U8 playlists (remote URL or local file)
- Xtream-compatible login with one or more server/base URLs, per-server
  diagnostics and provider-block (HTTP 884) classification
- Movies (VOD) and TV series with details, filters and search, where your
  provider supplies them
- XMLTV EPG guide with Now/Next and a guide screen
- Favorites, watch history, continue watching and resume
- Native browser playback plus an optional maximum-compatibility playback
  engine (managed FFmpeg components, installed on request from Settings)
- Seeking — including distant seeking while a compatibility conversion is
  still in progress — and reconnect recovery that returns to your position
- Sanitized playback-report export for troubleshooting (no provider URLs or
  credentials)
- Local backups, reset tools, and local-first storage with credential masking
- In-app update check and verified update download (user-triggered, never
  forced)

## Application updates

From this release onward the app can check for updates itself:
**Settings → Application updates**. Updates are checked and downloaded only
when you ask, verified against an exact size and SHA-256 checksum before
anything happens, and never installed while something is playing. On unsigned
builds the install step is honest: the app quits and opens the verified
package so you can drag it into Applications yourself.

## Reporting a problem

If a stream misbehaves, export a sanitized playback report from the player's
diagnostics panel or from **Settings → Troubleshooting report**, then attach
the ZIP when you open an issue on this repository. The report contains no
playlist or provider URLs, hostnames, usernames, passwords, tokens or file
paths — the app refuses to write the file if anything secret-shaped remains.

## Important legal notice

FoS IPTV is only a player. It does not provide IPTV service, channels,
movies, series, subscriptions, provider accounts, credentials, playlists, or
access to paid content, and it never bypasses DRM, geo-blocking, paywalls,
tokens, device locks or any other provider restriction.

You are responsible for making sure you have the legal right to access
anything you add to the app. Do not use FoS IPTV to access pirated, stolen,
unauthorized or otherwise restricted content.

## Privacy

FoS IPTV collects no telemetry and phones nothing home. Your sources,
credentials and history stay on your machine; the app talks only to the
providers you configure, to the clearly-labeled public demo test streams if
you try demo mode, and to this repository when you ask it to check for
updates or install optional playback components. Exported playback reports
are saved locally and sent only if you choose to send them.

## License

FoS IPTV is free to use and proprietary (closed source). See LICENSE.md in
this repository.
