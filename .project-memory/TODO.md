# Pending Improvements & Tasks

This file tracks suggested improvements, template cleanups, and follow-up tasks for repository maintainers.

## Bucket Configuration & Metadata

- [ ] **Configure repository upstream in `bin/auto-pr.ps1`**:
  Replace `[String]$upstream = "<username>/<bucketname>:main"` with the actual repository coordinates (e.g. `bitoolean/scoop-bucket:master`).
- [ ] **Replace placeholders in `README.md`**:
  - Update GitHub action badges in lines 3–4 (replace `<username>/<bucketname>`).
  - Update usage and install instructions in line 48 (`scoop bucket add <bucketname> https://github.com/<username>/<bucketname>`).
- [ ] **Add an Applications catalog table to `README.md`**:
  Provide a quick summary table listing currently available manifests (`git-updater`, `local-desktop-store`), version, upstream project links, and short descriptions for users browsing the bucket.

## GitHub Workflows & Automation

- [ ] **Verify default branch alignment in CI/Excavator**:
  Ensure `.github/workflows/ci.yml` and `.github/workflows/excavator.yml` align with the repository default branch (`master` vs `main`).
- [ ] **Verify Excavator workflow permissions**:
  Ensure GitHub Actions has "Read and write permissions" enabled under repo Settings -> Actions -> General -> Workflow permissions so Scoop's Excavator can push auto-update commits or open PRs.

## Manifests

- [ ] **Validate manifests via Scoop test suite**:
  Run `Scoop-Bucket.Tests.ps1` once a full local Scoop development/test harness is set up.
- [ ] **Track .NET 9 lifecycle for `local-desktop-store`**:
  Revisit runtime requirement when upstream moves past .NET 9 (reaches end-of-support in November 2026).
