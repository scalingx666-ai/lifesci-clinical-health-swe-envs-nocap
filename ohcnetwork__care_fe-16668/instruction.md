# Issue

**Title:** Update Permissions-Policy for microphone access

## Description

## Proposed Changes

Hot-fix

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Enhancements**
  * Updated browser permissions to allow geolocation and microphone access on the same origin.
  * Improved production builds so security headers are generated and applied automatically after building.
* **Bug Fixes**
  * Corrected header configuration to consistently enable microphone access for same-origin features.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bf62b0123497`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.