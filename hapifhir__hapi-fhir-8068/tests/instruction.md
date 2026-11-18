# Issue

**Title:** Skip installing older package versions in the same package install call

## Description

When installing a FHIR package whose dependency tree pulls in multiple versions of the same package, resources could be silently downgraded. This PR adds two levels of protection:

**Solution**

Package-level: A new `PackageDependencyRegistry` tracks installed dependency packages during installation. In `SINGLE_VERSION` mode, it detects redundant dependencies (exact duplicates and older versions) and skips them entirely.

Resource-level: A new `PackageVersionStamper` reads the meta.source field (stamped as `packageName|packageVersion` during installation) to compare incoming vs existing package versions. In `MULTI_VERSION` mode (default), this protects `SearchParameter` resources which match by code and base rather than URL and version. In `SINGLE_VERSION` mode, all canonical resources are protected.

**Changes**
  
  - `PackageInstallerSvcImpl` — Added skip logic in install() and fetchAndInstallDependencies() using the two new classes
  - `PackageVersionStamper` (new) — Handles `meta.source` stamping, parsing (using existing `UrlUtil.parseCanonicalUrl())`, and version comparison
  - `PackageDependencyRegistry` (new) — Tracks highest installed version per package name, detects redundant dependencies
  - `packages.md `— Added "Version Policy" section documenting `MULTI_VERSION` vs `SINGLE_VERSION` behavior and redundant dependency handling

**Test plan**

  - `PackageVersionStamperTest` — 13 unit tests for stamping, parsing, and version comparison
  - `PackageDependencyRegistryTest` — 9 unit tests for dependency tracking and redundancy detection
  - `PackageInstallerSvcImplTest` — 8 integration tests covering `SearchParameter` skip, `CodeSystem` passthrough/skip, request-id in `meta.source`, and cross-package scenarios

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `56e2ebc285ce`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.