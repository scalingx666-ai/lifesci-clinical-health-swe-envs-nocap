# Issue

**Title:** fix(backend): keep a data source's name and software version current

## Description

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Software versions advance only when a newer dotted numeric version is received. If no version is stored, incoming values—including invalid ones—can be accepted.
  * App-keyed sources can adopt a different source name when it is not the app ID. Device-keyed source names remain unchanged when the incoming name matches the device model.
  * Added regression coverage for source-name handling and software-version updates.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4de8b0833e80`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.