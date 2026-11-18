# Issue

**Title:** RELEASE 992 XML Preprocessing updates

## Description

Issues:

- https://linear.app/metriport/issue/ENG-992

### Description

-  

### Testing

Check each PR.

### Release Plan

- :warning: Points to `master`
- [x] Merge this
- [x] Reprocess some of the affected patients

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Automatic sanitization of CDA XML before conversion, improving support for varied CDA files.
  * Unified S3 fetch-and-validate flow with clearer validity outcomes.

* **Bug Fixes**
  * Reduced conversion failures caused by problematic XML processing instructions.
  * Prevented errors when no Base64 attachments are present.
  * More robust handling and messaging for non-convertible documents.

* **Refactor**
  * Streamlined conversion pipeline by replacing legacy convertibility logic and simplifying XML parsing, improving reliability without changing public interfaces.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `336950c93497`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.