# Issue

**Title:** Fix Windows multimodal fixture and test portability

## Description

## Description

Fix the Windows failures in the full v3.3 suite after the multimodal PRs landed.

## Type of Change

- [x] Bug fix
- [x] Documentation update
- [x] Test improvement

## Changes Made

- Read the signed ambient FHIR fixtures as UTF-8.
- Hash the fixed OpenPHI-Vision text catalog with LF line endings so Windows checkouts produce the pinned digest. The font and rendered pixel digests retain their byte-level checks.
- Build notice-registry module names from path components and pass test subprocess paths as arguments.
- Download the checksum-pinned Gitleaks, Trivy and Syft archives through GitHub's release-asset API after the direct downloads returned HTTP 504.

## Testing

- Canonical formatting, lint, effect inventory and formatting verification passed.
- 176 focused tests passed, including the CRLF catalog check and subprocess tests with backslashes and spaces in their temporary paths.
- Full local Python suite passed with 29,766 tests. Strict docs build passed.
- Workflow lint, 89 focused release and security tests, and SHA-256 verification for the three Linux scanner archives passed.
- The `full-ci` label selects both Windows full-suite jobs.

## Dependencies

The existing dependencies cover the repair.

## Related Issues

 and #4126.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b0e2f455ba3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.