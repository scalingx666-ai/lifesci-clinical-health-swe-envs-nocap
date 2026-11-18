# Issue

**Title:** Require patched ASN.1 decoding in the cloud extra

## Description

## Description

The v3.2 candidate's vulnerability gate blocks on four HIGH pyasn1 decoder advisories in the optional cloud closure. Require `pyasn1>=0.6.5` in the cloud extra and uv constraints, and update only that package's locked version and artifact hashes. The [upstream release](https://github.com/pyasn1/pyasn1/releases/tag/v0.6.5) fixes CVE-2026-119194 through CVE-2026-119197.

## Type of Change

- [x] Bug fix
- [x] Documentation update

## Changes Made

- Add the patched minimum to the published cloud extra.
- Retain the existing lockfile format and every unrelated package record, platform marker and pin.
- Document the change in the v3.2 changelog and release notes. Core dependencies, scanner policy and allowlists are unchanged.

## Testing

- [x] CI's uv 0.13.6 accepts `uv lock --check --offline` without drift; a frozen cloud install of the final lock succeeds.
- [x] Existing scanner/pip-audit policy, cloud storage, dependency report and core-import tests: 110 passed and 20 passing subtests.
- [x] Networking-blocked smoke check: cloud imports, ASN.1 DER round trip, synthetic service-account signing and JWT verification pass with pyasn1 0.6.5 / pyasn1-modules 0.4.2 / google-auth 2.55.1.
- [x] Canonical formatting, lint, format check, scoped pre-commit and strict complete docs staging pass.
- [x] Wheel/sdist build and Twine checks pass; wheel metadata scopes the new floor to `extra == cloud`.
- [x] Full final candidate suite after the license follow-ups: 24,224 passed, 158 skipped and 11,344 passing subtests.
- [x] All 21 final hosted workflows pass on #4369 at `53ca5a6d01fc0e8a2cf8a503e7400e828e6592f6`, including the unchanged vulnerability scan, full Python/SDK matrix, Nix and documentation/browser checks.

Maintainer follow-ups in #4369 also record the upstream BSD-2-Clause license in both reviewed inventories. The inventory test now checks exact declared-dependency coverage; missing/restricted negative controls still block. All 61 inventory/license/repository-policy tests and 26 subtests pass.

## Dependencies

This adds a security floor for an existing transitive cloud dependency. No package is added to the core dependency set and no other locked version changes.

## Related Issues

. Targets `prepare/v3.2.0` for inclusion in #4369.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `645260548784`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.