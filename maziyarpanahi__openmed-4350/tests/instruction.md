# Issue

**Title:** Fix service-image builds with current timezone data pin

## Description

## Description

Service-image builds stop at APT because Debian Forky replaced `tzdata=2026e-1` with `2026f-1`. The failure prevents the image SBOM and vulnerability jobs from reaching their image checks.

Update that exact pin in both the root Dockerfile and the published multi-architecture Dockerfile. Their runtime recipes remain aligned.

## Type of Change

- [x] Bug fix

## Validation

- Verified the live amd64 and arm64 Forky package indexes: timezone data is the only unavailable APT pin.
- Downloaded the architecture-independent replacement and verified its published SHA-256: `7ef210d4dfaca780b16cfbd307c4a38d0408b24e6774bde541a45b8ffe742b9f`.
- Focused container/security/SBOM checks: 70 passed, 17 subtests.
- Complete suite: 23,004 passed, 151 skipped, 11,220 subtests in 196.25 seconds.
- Canonical checks, strict docs, three Chromium guards and package build: passed on `f07474ea22e3fcd80a61129a2fa1594b867f0b60`.

Hosted validation also passed on this exact head: the linux/amd64 image build and smoke test, ARM64 SMS latency budget, image SBOM generation, and the image/lockfile vulnerability gate. Other platform test jobs were still running with no failures reported at review.

## Documentation

Added an Unreleased changelog note. This change retains the existing base digests, other package pins and security gates.

## Related Issues

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9dd9f2c77079`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.