# Decisions

## Manifest naming convention

Scoop package and manifest names follow the official Scoop guidelines and community standard conventions:
- Use **kebab-case** (all-lowercase letters, digits, and hyphens `-`).
- Separate compound words or title-cased upstream product names with hyphens (e.g. `LocalDesktopStore` -> `local-desktop-store`).
- Keep package names concise and avoid redundant suffixes like `-Portable` or `-standalone` unless differentiating multiple packaging variants in the same bucket (portable is already the default Scoop expectation).

## Workflow convention

- When confirmed changes include project files (e.g. manifests, scripts, configurations, docs), commit and push them along with any accompanying `.project-memory` updates to the remote repository.
- Changes made solely to the `.project-memory` directory do not trigger a push on their own.

## GitHub release-asset hashes

For GitHub-hosted release assets, use GitHub's immutable `asset.digest` as the
autoupdate hash source when the release API supplies it.

```json
"hash": {
    "url": "https://api.github.com/repos/OWNER/REPO/releases/tags/v$version",
    "jsonpath": "$.assets[?(@.name == 'ASSET-NAME-$version.zip')].digest"
}
```

GitHub returns values in `sha256:<hex>` form. Current Scoop autoupdate handling
strips the `sha256:` prefix. Keep the normal explicit `hash` field for the
manifest's currently pinned version, using the verified current asset digest.

Use an exact asset-name predicate for each architecture. This avoids relying on
release-page markup or downloading a release solely to calculate its checksum.

## LocalDesktopStore packaging

`bucket/local-desktop-store.json` targets
`LocalDesktopStore-v$version-win-x64.zip`. It is the plain
framework-dependent build and does not require elevation. It
requires the .NET 9 Desktop Runtime for Windows x64.

The manifest uses a `pre_install` guard rather than a Scoop `depends` entry
because the official Versions bucket has no .NET 9 Desktop Runtime manifest. The guard
checks `dotnet --list-runtimes` for `Microsoft.WindowsDesktop.App 9.0.*` and
throws a clear actionable error when it is absent, including in callers that
surface Scoop installation failures.

The manifest notes explicitly document that the application's runtime data and
downloaded app catalog reside in `%LOCALAPPDATA%\LocalDesktopStore` and are
not portable across systems. The Velopack portable variant is intentionally
omitted from the bucket.

## Linkquisition packaging

`bucket/linkquisition.json` targets `Linkquisition_Windows_amd64.zip` (the
non-installer portable archive from Strobotti/linkquisition).

- **Hardware Acceleration / OpenGL DLL**: The release archive bundles Mesa's
  software OpenGL fallback (`opengl32.dll`). The manifest removes `opengl32.dll`
  via `post_install` so the application utilizes the system's hardware GPU drivers.
  The manifest description explicitly notes that a GPU is required.
- **Default Browser Registration**: Notes explain that setting Linkquisition
  as default browser / HTTP handler can be done via `linkquisition set-default`
  or directly from its graphical interface.

## YourCopilotBrowser packaging

Both YCB manifests use the upstream `YCB-Setup.exe` release asset with Scoop's
7-Zip extractor. The upstream `YCB-Setup.zip` is an outer ZIP containing the
same installer executable, so the manifests avoid that extra wrapper.

`ycb-lean` is a manifest-level workaround, not a separate upstream
framework-dependent build. Its `pre_install` checks for the .NET 8 Desktop
Runtime, rewrites the bundled runtime configuration to framework-dependent
mode, removes runtime-pack `runtime` and `native` assets and metadata, and
cleans installer artifacts and localization directories. The current release
requires .NET 8 Desktop Runtime 8.0.27 or later. Recheck these assumptions when
the upstream release format or runtime-pack metadata changes.

## GitHub Actions token permissions

Keep the repository's default `GITHUB_TOKEN` permission read-only. The
Excavator workflow explicitly requests `contents: write`; GitHub applies
workflow/job permissions after the default, so updates get only the write
access they need without granting it to every workflow by default.
