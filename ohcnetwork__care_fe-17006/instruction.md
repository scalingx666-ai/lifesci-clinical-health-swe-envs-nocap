# Issue

**Title:** Use ENG-737-backup for the Playwright backend

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/135/changes/care_fe/135
<!-- entire-trail-link-end -->

## Proposed Changes

Switch the Playwright CI backend default from `ENG-737` to `ENG-737-backup` and update the testing guide. Manual `backend_ref` overrides continue to work.

## Validation

Verified that the remote backend branch exists at `d4e34f4311387d16d2020f0e0f4794fb415caa83`. Workflow YAML parsing, checkout-reference verification, Prettier, diff checks, and independent review passed. This changes only the backend selection and documentation; application tests were not rerun.

No backend source or remote branch changes are included.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8cc23754eb6c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.