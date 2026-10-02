# bitoolean's Scoop bucket

[![CI](https://github.com/bitoolean/scoop-bucket/actions/workflows/ci.yml/badge.svg)](https://github.com/bitoolean/scoop-bucket/actions/workflows/ci.yml)
[![Excavator](https://github.com/bitoolean/scoop-bucket/actions/workflows/excavator.yml/badge.svg)](https://github.com/bitoolean/scoop-bucket/actions/workflows/excavator.yml)

A third-party [Scoop](https://scoop.sh) bucket for Windows applications and
utilities.

## Applications

| Name | Architecture | Info |
| --- | --- | --- |
| [git-updater](bucket/git-updater.json) | 64-bit, ARM64 | [On-demand desktop GUI for updating apps from GitHub releases](https://github.com/TeeJS/git-updater) |
| [Linkquisition](bucket/linkquisition.json) | 64-bit | [Browser picker and URL dispatcher](https://github.com/Strobotti/linkquisition) |
| [LocalDesktopStore](bucket/local-desktop-store.json) | 64-bit | [Private Windows app catalog sourced from GitHub Releases](https://github.com/SysAdminDoc/LocalDesktopStore); requires the .NET 9 Desktop Runtime. Its app data is stored in LocalAppData. |
| [YCB](bucket/ycb.json) | 64-bit | [YourCopilotBrowser](https://github.com/Tomcreations/YourCopilotBrowser), a lightweight Windows browser running on top of the Microsoft Edge WebView2 Runtime. |
| [YCB lean](bucket/ycb-lean.json) | 64-bit | YourCopilotBrowser without its bundled .NET runtime; requires the .NET 8 Desktop Runtime and WebView2. |

## Install

Add the bucket and install an application by its manifest name:

```pwsh
scoop bucket add bitoolean https://github.com/bitoolean/scoop-bucket
scoop install bitoolean/git-updater
```

## Contributing

For manifest contributions, see the [Scoop contributing guide](https://github.com/ScoopInstaller/.github/blob/main/.github/CONTRIBUTING.md)
and the [App Manifests wiki](https://github.com/ScoopInstaller/Scoop/wiki/App-Manifests).
