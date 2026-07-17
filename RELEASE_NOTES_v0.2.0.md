# FoS IPTV v0.2.0 — unsigned macOS test build

This is the second public test release of FoS IPTV, published through
[FoSGamers/FoS-IPTV-Releases](https://github.com/FoSGamers/FoS-IPTV-Releases).

Important: this is an **unsigned** and non-notarized macOS test build. It is
meant for early testers before the app has full Apple Developer ID signing
and notarization. It is for Apple Silicon Macs only (mac-arm64); no Windows,
Intel-Mac, or Linux package is part of this release.

## What to download

Two packages are published, both Apple Silicon (mac-arm64) builds of the same
app:

- `FoS-IPTV-0.2.0-mac-arm64.dmg` — open it and drag **FoS IPTV** into
  **Applications** (recommended).
- `FoS-IPTV-0.2.0-mac-arm64.zip` — unzip it and move **FoS IPTV.app** into
  **Applications**.

The exact SHA-256 checksum and byte size of each package are recorded in the
release's update manifest, so a download can be verified before it is opened.

## macOS damaged-app warning

macOS may show this warning:

> "FoS IPTV" is damaged and can't be opened. You should move it to the Trash.

That happens because this build is not signed or notarized yet — macOS
quarantines downloaded, unsigned apps. It does not mean the download is
broken. After installing, clear the quarantine attribute once in Terminal
(adjust the path if the app is not in Downloads):

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

This release is for Apple Silicon Macs only (M1/M2/M3/M4). It is not for
Intel Macs. To check your Mac type, run `uname -m` — the expected result is
`arm64`.

## What's new in v0.2.0

v0.2.0 collects a substantial body of playback-reliability work completed
since the first public test build. The headline is managed compatibility
playback: movies and episodes that need the FFmpeg compatibility engine now
behave predictably from start to finish.

- **Managed compatibility playback.** Media that plays through the FFmpeg
  compatibility engine is driven end to end by the app instead of drifting on
  raw engine behavior, so start, seek, and recovery all behave consistently.
- **Buffering and starvation corrections.** A source that arrives slower than
  real time shows an honest buffering state and resumes cleanly instead of
  stalling or racing ahead of the data it actually has.
- **Stable compatibility-VOD duration.** A converting movie shows its full,
  stable duration from the first frame; the timeline no longer grows as the
  conversion catches up.
- **Distant / random-access seeking.** You can seek to any point in a
  compatibility-VOD, including far ahead. Seeking within the converted part is
  instant; a more distant point briefly shows a "preparing" state while
  playback is set up at that position — without converting everything in
  between.
- **Reconnect recovery preserves source position.** A brief reconnection
  resumes near where you were, not back at the start.
- **Paused and playing recovery intent.** Recovery honors whether you were
  playing or paused, including the case where a new stream was ready but had
  been left paused on a spinner.
- **Progress-bar stability during reconnect.** Throughout recovery the
  progress bar holds at the position you requested instead of snapping to the
  beginning, then continues from there once the stream is ready.
- **Sanitized playback-report export.** If something misplays, you can export a
  playback report from the player's diagnostics panel or from Settings and send
  it to the developer. It contains no provider URLs or credentials.
- **Truthful pending / completed recovery diagnostics.** The report leads with
  a plain recovery status and outcome — whether a recovery is still in
  progress, whether your position was preserved (measured at the moment
  playback re-attached, so normal playback afterward is reported separately and
  never mistaken for lost position), and whether recovery resumed automatically
  or you resumed it yourself later.
- **Operation-scoped report outcomes.** Recovery outcomes are scoped to the
  operation that produced them, so one recovery's result is never attributed to
  a later, unrelated playback event.
- **In-app application updates.** New in this release: **Settings →
  Application updates** checks the public releases page on request, downloads
  only when you ask, verifies the exact size and SHA-256 checksum before
  anything happens, and never installs while something is playing. On unsigned
  builds the install step is honest — the app quits and opens the verified
  package for a drag-to-Applications finish.
- **Expanded automated release validation.** The release is gated by an
  expanded automated suite covering the packaged application, a packaged
  clean-install and offline upgrade proof, package-content inspection,
  security posture, and release-artifact/version consistency.

## Everything from the first release is still here

Live TV from your own M3U/M3U8 playlists (URL or local file), Xtream login
with multiple server URLs and per-server diagnostics (including HTTP 884
classification), movies and series where your provider supplies them, XMLTV
EPG with Now/Next and a guide screen, search, favorites, watch history and
resume, backups and reset tools, an offline demo mode with clearly-labeled
test streams, and local-first storage with credential masking throughout.

## Upgrading from v0.1.0

v0.1.0 has no in-app updater, so upgrade manually: download a v0.2.0 package
above, quit FoS IPTV, replace the old app in Applications with the new one,
and clear the quarantine flag again (the new download is quarantined too —
see the command above). In-app update checks exist from v0.2.0 onward, so
future releases can be discovered and downloaded from inside the app.

Your local data lives outside the app itself, so replacing the app keeps your
sources, favorites, settings, watch history, guide cache and installed
playback components. This is exercised by an automated packaged upgrade test
before release. Exporting a backup first (Settings → Your data & backup) is
still a sensible precaution.

## How this release was validated

Automated, all passing before publication: type checking, linting, unit
tests, renderer component tests, security tests, end-to-end user flows in the
built app, a packaged-app clean-install proof, an offline packaged upgrade
proof, package-content validation, and release-integrity/version-consistency
validation.

Separately, the final packaged candidate received a **limited manual launch
and smoke check** — it was installed, launched, and observed working as
before. It did **not** receive a complete manual regression test of every
feature; the automated suites above are the per-feature proof.

## Known limitations

- Unsigned and not notarized — macOS warns on first launch (workaround
  above).
- Apple Silicon macOS only; no Windows, Linux or Intel-Mac package in this
  release.
- Early public-test status; provider capabilities and compatibility vary, and
  blocked provider endpoints are reported honestly, never bypassed.
- Live streams can only buffer what the provider's live window exposes — no
  player can pre-download the future of a live stream.

## What FoS IPTV is

FoS IPTV is a free desktop IPTV player for users who already have their own
legal IPTV playlist or Xtream-compatible provider account. It ships with zero
content: you bring your own legal M3U/M3U8/Xtream/XMLTV sources, and you are
responsible for making sure your sources and usage are lawful.
FoS IPTV does not include, sell, discover, recommend, or provide television channels, movies, series, playlists, subscriptions, or provider accounts.
