# Current State

## Purpose

This repository is a personal Scoop bucket and companion scripts. Installable
manifests live in `bucket/`; unapproved proposals belong in
`.project-memory/drafts/`.

## Current Manifests

- `git-updater` 0.2.6: x64 and ARM64.
- `linkquisition` 3.1.10: x64 portable archive; post-install removes its bundled
  Mesa OpenGL fallback DLL.
- `local-desktop-store` 0.3.2: x64; requires the .NET 9 Desktop Runtime and
  stores app data under LocalAppData.
- `ycb` 1.0.26: unpacks the upstream `YCB-Setup.exe` directly. The release ZIP
  is an outer ZIP containing that same executable.
- `ycb-lean` 1.0.26: transforms the self-contained YCB package into a
  framework-dependent install by rewriting runtime configuration and removing
  runtime-pack files and metadata. Requires .NET 8 Desktop Runtime 8.0.27 or
  later.

## Validation

- The repository `bin/checkver.ps1` wrapper successfully ran the installed
  Scoop core `bin/checkver.ps1` against all five manifests. `checkver` is not a
  registered `scoop` command in this installation.
- CI passed on commit `976935d`.
- The YCB Lean cleanup was tested through an isolated debug manifest: 238
  runtime-pack files, runtime-pack metadata, the `runtimes` directory, and
  installer-created `$` directories were removed from the debug install.

## Ongoing Work

- Revisit LocalDesktopStore's .NET 9 runtime requirement before support ends in
  November 2026 or when upstream moves to a newer runtime.
- Revalidate YCB Lean's packaging conversion when upstream changes the release
  archive or .NET runtime-pack layout.
