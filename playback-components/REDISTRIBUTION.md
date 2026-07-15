# FoS IPTV — playback component redistribution & licensing review

FoS IPTV is a media **player**. It ships with **no content** and provides no
IPTV service. The optional native playback components below extend the range of
formats the player can decode; they are downloaded on demand by the in-app
playback component manager (PLY-32) and are **never bundled inside the app**.

This document is the redistribution review required before publishing any of
these third-party binaries. It records the exact builds, their licenses, and
the corresponding-source obligations that this repository satisfies.

## What is distributed

Downloaded on demand, per platform, verified in-app by SHA-256 + executable
magic-bytes + a `-version` self-identification check before use:

| Component | Role | Platforms | Version | License |
| --- | --- | --- | --- | --- |
| FFmpeg   | container/codec conversion (required for compatibility playback) | mac-arm64, mac-x64, win-x64, linux-x64 | 8.1.2 | GPLv3 |
| FFprobe  | stream analysis (required for compatibility playback)            | mac-arm64, mac-x64, win-x64, linux-x64 | 8.1.2 | GPLv3 |
| mpv      | maximum-compatibility external player (optional)                 | win-x64 | 0.41.0 | GPLv2-or-later |

mpv is not yet offered for macOS or Linux: no verified self-contained,
relocatable single-binary build was available at review time. The app reports
this honestly ("This component is not yet available for your platform.") and
those platforms fall back to the FFmpeg compatibility backend. mpv coverage
will expand as verified builds are reviewed.

## Exact builds and their upstream sources

The binaries here are **redistributed verbatim** from these upstream builders.
Because FFmpeg and mpv are GPL, the corresponding source must remain available;
each upstream publishes both the component source and the exact build recipe.

- **FFmpeg / FFprobe 8.1.2 — macOS (arm64, x64):** static release builds by
  Martin Riedl. Build service: <https://ffmpeg.martin-riedl.de/>. FFmpeg source:
  <https://github.com/FFmpeg/FFmpeg> (release/8.1, tag `n8.1.2`). These builds
  link GPL libraries (x264/x265), so the combined work is **GPLv3**.
- **FFmpeg / FFprobe 8.1.2 — Windows x64, Linux x64:** BtbN FFmpeg-Builds,
  `win64-gpl` / `linux64-gpl` variant, `n8.1.2-22-g94138f6973`. Build recipe:
  <https://github.com/BtbN/FFmpeg-Builds>. FFmpeg source:
  <https://github.com/FFmpeg/FFmpeg>. GPL variant → **GPLv3**. The upstream
  archives include the GPLv3 text (mirrored here as `LICENSES/FFmpeg-GPLv3.txt`).
- **mpv 0.41.0 — Windows x64:** shinchiro mpv-winbuild-cmake release
  `20260610` (`mpv-x86_64-20260610-git-304426c`). Build recipe:
  <https://github.com/shinchiro/mpv-winbuild-cmake>. mpv source:
  <https://github.com/mpv-player/mpv>. mpv is **GPLv2-or-later** (mirrored here
  as `LICENSES/mpv-GPLv2.txt`).

## License obligations and how this repo meets them

1. **License text accompanies the binaries.** The GPLv3 and GPLv2 texts are in
   `playback-components/LICENSES/`. They are cited from the in-app "Playback
   compatibility" documentation and this file travels with every release.
2. **Corresponding source stays available.** FFmpeg and mpv source, and the
   exact build recipes, are the public upstream repositories linked above; this
   review pins the exact versions/tags so the corresponding source for each
   redistributed binary is identifiable and obtainable. This constitutes the
   written offer of source under the GPL.
3. **No modification, no relinking.** Binaries are redistributed byte-for-byte
   from upstream (verified: the SHA-256 in `manifest.json` is the SHA-256 of the
   exact file published here). FoS IPTV does not patch, strip, or relink them.
4. **No proprietary combination.** The components run as **separate processes**
   invoked over an argument-array command line (never linked into the Electron
   app), so the app's own license is unaffected and no GPL obligation extends to
   the FoS IPTV application code.
5. **Player, not a provider.** These components decode user-supplied media only.
   Nothing here provides content, and nothing bypasses DRM, geo-restrictions,
   provider authentication, or any access control.

## Integrity chain

`manifest.json` lists, per component × platform: the dotted version, the
GitHub release download URL, the SHA-256, and the exact byte size. The in-app
manager fetches the manifest over HTTPS from a pinned FoS/GitHub host, downloads
each artifact from a pinned URL (revalidating every redirect hop), and refuses
to install anything whose SHA-256, executable type, or `-version` identity does
not match. The manifest is not yet cryptographically signed — signing with an
app-embedded key is the tracked follow-up (see FoS IPTV DECISION_LOG ADR-028).
