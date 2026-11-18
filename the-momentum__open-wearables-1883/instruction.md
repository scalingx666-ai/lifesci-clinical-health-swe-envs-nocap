# Issue

**Title:** refactor(frontend): dark theme accent color & general design changes

## Description

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Style**
  * Updated the dark primary color and chart series colors to use a consistent palette. Unlisted chart series use a grey tone.
  * Avatars, provider marks, and stat icons now use consistent neutral styling; vital trend accents use the primary color.
  * Connection badges use a neutral appearance. Expired and revoked connections are distinguished by status dots, with accessible status text.
* **Tests**
  * Updated chart color checks to verify that series colors avoid status-color tones.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `67cee1d59574`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.