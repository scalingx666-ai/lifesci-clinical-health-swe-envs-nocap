# Issue

**Title:** [ENG-846] fixes error handling in batch request

## Description

copy of #16635

> this was reviewed by multiple people in #16635

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added improved batch-request handling with atomic rollback, per-request error details, and optional suppression of automatic error messages.
  * Preserved access to failed results and original errors for more reliable error recovery.

* **Bug Fixes**
  * Prevented medication-dispensing update failures from displaying an unwanted error notification.

* **Documentation**
  * Added guidance and examples for using batch requests, including pending states and failure handling.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5878887e115`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.