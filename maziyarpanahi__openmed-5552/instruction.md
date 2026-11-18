# Issue

**Title:** fix: restore release image SBOMs and patch blocked dependencies

## Description

## Description

Fix the failed v3.3.0 image SBOM job: the live Debian mirror no longer offers the pinned SQLite package. Both Dockerfiles now resolve the existing exact runtime pins from a dated, signed Debian snapshot. Base-image digests and runtime package pins remain unchanged.

Release SBOMs now inventory the published container by immutable digest after verifying its SLSA provenance against the release tag, commit, repository, and publishing workflow. A master-only recovery input attaches the validated SBOM, checksum, and source-binding record to an existing release. The pinned Syft download uses the job token and retains its mandatory checksum verification.

Required security gates also exposed vulnerable dependencies. Upgrade Soup Sieve to 4.0, OpenTelemetry API/SDK to 1.45.2, and coupled semantic conventions to 0.66b2. **The minimum Python patch version becomes 3.11.5**, matching Soup Sieve's requirement. Standalone packaging, dependency contracts, testing docs, and the Unreleased changelog reflect that floor. No security thresholds, ignore lists, privacy assertions, or test tiers are weakened.

Related failure: https://github.com/maziyarpanahi/openmed/actions/runs/43475274183/job/132057371723

## Change type

- [x] Bug fix
- [x] Build/release repair
- [x] Documentation update

## Validation

- Final full local suite: **29,831 passed, 241 skipped, 11,404 subtests passed**, zero failures.
- Focused release/provenance/tracing/privacy/security regressions: 90 passed and 25 subtests passed.
- Unchanged pip-audit gate: no known vulnerabilities found.
- Canonical formatting, lint, effect-path validation, format check, actionlint, lockfile check, license policy, wheel/sdist builds, and strict docs build passed.
- Verified wheel metadata contains the new Python floor and patched API requirement.
- Fresh uncached amd64 and arm64 runtime builds passed SQLite/TLS smoke checks.
- Verified the existing v3.3.0 published image's provenance against its original commit and tag.
- All final-head hosted checks pass, including CI, Nix, docs/browser validation, Image SBOM, Container Multi-Arch, Vulnerability Scan, lock gate, attribution, conformance, and SDK release-candidate checks. Docs/browser validation passed on retry after a Firefox controls test exhausted its existing shared 45-second budget; its assertions and timeouts remain unchanged.

## Dependency justification

Soup Sieve 4.0 fixes [CVE-2026-126190](https://github.com/facelessuser/soupsieve/security/advisories/GHSA-mmhr-3c5m-f64f). OpenTelemetry 1.45.2 fixes the oversized traceparent parsing issue reported as CVE-2026-126360; see the [upstream changelog](https://github.com/open-telemetry/opentelemetry-python/blob/main/CHANGELOG.md#version-1452066b2-2026-10-29). Only the patched packages and directly required coupled packages change version; obsolete conditional async-timeout is removed.

## Docs and release recovery

Updated the SBOM recovery instructions and testing requirements. Recovery preserves the existing v3.3.0 tag and does not republish Python, npm, or container packages.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8097fc0bbaad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.