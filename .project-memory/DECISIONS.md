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
