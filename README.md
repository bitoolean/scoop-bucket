# bitoolean's Scoop bucket

[![CI](https://github.com/bitoolean/scoop-bucket/actions/workflows/ci.yml/badge.svg)](https://github.com/bitoolean/scoop-bucket/actions/workflows/ci.yml)
[![Excavator](https://github.com/bitoolean/scoop-bucket/actions/workflows/excavator.yml/badge.svg)](https://github.com/bitoolean/scoop-bucket/actions/workflows/excavator.yml)

A third-party [Scoop](https://scoop.sh) bucket for Windows applications and
utilities.

## Applications

| Manifest | Architecture | Application |
| --- | --- | --- |
| [git-updater](bucket/git-updater.json) | 64-bit, ARM64 | [On-demand desktop GUI for updating apps from GitHub releases](https://github.com/TeeJS/git-updater) |
| [linkquisition](bucket/linkquisition.json) | 64-bit | [Browser picker and URL dispatcher](https://github.com/Strobotti/linkquisition); GPU required for hardware-accelerated rendering. |
| [local-desktop-store](bucket/local-desktop-store.json) | 64-bit | [Private Windows app catalog sourced from GitHub Releases](https://github.com/SysAdminDoc/LocalDesktopStore); requires the .NET 9 Desktop Runtime. Its app data is stored in LocalAppData. |
| [ycb](bucket/ycb.json) | 64-bit | [YourCopilotBrowser](https://github.com/Tomcreations/YourCopilotBrowser); the manifest extracts the `YCB-Setup.exe` release directly rather than using the ZIP wrapper around that executable. Requires WebView2. |
| [ycb-lean](bucket/ycb-lean.json) | 64-bit | YourCopilotBrowser with a nonstandard manifest conversion from self-contained to framework-dependent deployment. It rewrites runtime metadata and removes bundled runtime assets; requires .NET 8 Desktop Runtime 8.0.27 or later and WebView2. |

## Install

Add the bucket and install an application by its manifest name:

```pwsh
scoop bucket add bitoolean https://github.com/bitoolean/scoop-bucket
scoop install bitoolean/git-updater
```

## Contributing

For manifest contributions, see the [Scoop contributing guide](https://github.com/ScoopInstaller/.github/blob/main/.github/CONTRIBUTING.md)
and the [App Manifests wiki](https://github.com/ScoopInstaller/Scoop/wiki/App-Manifests).
