# Current State

## Purpose

This repository is a personal Scoop bucket and companion setup scripts. The
installable manifests live in `bucket/`; `TODO/` holds prospective or unfinished
manifests.

## Current Work

- Added `bucket/git-updater.json` for TeeJS/git-updater v0.2.6, supporting x64
  and ARM64.
- Added `bucket/local-desktop-store.json` for SysAdminDoc/LocalDesktopStore
  v0.3.2. Its pre-install guard reports a missing .NET 9 Desktop Runtime
  explicitly.
- Both manifest files parse as JSON. The release tags, asset names, and initial
  SHA-256 values were verified through GitHub's Releases API.

## Next Tasks

- Revisit LocalDesktopStore's runtime requirement when the upstream project
  moves away from .NET 9, which reaches end of support in November 2026.
- Validate new manifests with Scoop's bucket tests where an appropriate Scoop
  development environment is available. The local Scoop installation does not
  provide the `checkver` command and its user config is outside this workspace.
