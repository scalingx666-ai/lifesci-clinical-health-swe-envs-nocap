# Issue

**Title:** Integrate signed offline language bundles and transactional activation

## Description

## Description

Integrate signed offline language bundles and transactional registry activation as one independently reversible change.

## Included pull requests

- #4288 — signed offline bundle packaging, installation and removal.
- #4292 — validated activation, generation handoff and rollback.

## Issues resolved

## Maintainer integration changes

- Bind the manifest parsed by the offline installer to the complete manifest verified by the shared signature verifier.
- Guard registry activation while notifying listeners, reject reentrant registration and restore both registry contents and generation on a failed notification.
- Exercise the complete packaging-to-activation handoff in the existing offline integration runner: verify signed policy/evidence files, measure installed model bytes, activate, roll back and refuse a digest mismatch.
- Document the explicit inner activation manifest and outer archive contracts, including read-once digest binding and their separate trust keys.

## Type of change

- [x] New feature
- [x] Bug fix
- [x] Documentation update

## Validation

The actual integration tree matches the passing local rehearsal exactly. Rehearsal: 142 focused tests; full suite 22,551 passed, 177 skipped and 11,209 subtests passed; canonical formatting/lint checks; strict MkDocs build; all three homepage/clinical analytics browser guards; wheel/sdist build and packaged-byte checks for five changed Python modules.

Exact final head `5811fcd9d6a41ebff0e0da5760ff3ac198865c69`: 142 focused tests; full suite 22,551 passed, 177 skipped and 11,209 subtests passed (190.18 seconds); `make format`, `make lint`, `make format-check`, `make docs-build`, all three Chromium artifact/analytics guards, `uv build` and five packaged-module byte comparisons passed.

Hosted checks were inspected on this SHA with no failures; some checks are still running. `master` is unprotected with no required status contexts. The complete local suite and scope-specific gates above provide the exact-head validation. Synthetic fixtures establish software behavior; they do not establish clinical validation.

## Dependencies and documentation

No new dependencies. Updated language pack and low-bandwidth installation documentation and Unreleased changelog entries.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `effc859d8bba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.