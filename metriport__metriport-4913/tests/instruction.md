# Issue

**Title:** ENG-1337 Various XML preprocessing and FHIR converter fixes

## Description

Part of 1337

### Description

- Various preprocessing fixes:
  - Better null flavor replacement algorithm
  - Better handling of `<` and `>` outside the XML tags
- Various converter fixes:
  - Printing file name on failure
  - Some minor type safety bug fixes -> responsible for many files failing to convert
- Added some unit tests 

### Testing
- Local
  - [x] Converted many files from the DLQ
  - [x] Ran full test suite
    - Got a slight increase in the resource counts. This is because the previous iteration of XML preprocessing was making one section of 4 test files invalid and cause it to be skipped over during conversion. The new algorithm restored that section in all 4 files, resulting in more data being successfully extracted! 🙌 
- Production
  - [ ] Reconvert some affected patients
  - [ ] Rerun DLQ

### Release Plan
 - [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Tests**
  * Added comprehensive tests for XML handling: comments, quoted attributes, nested/escaped characters, and null-flavor ID conversions across varied spacing and cases.

* **Bug Fixes**
  * Improved XML escaping and parsing around comments and attributes to prevent markup corruption and preserve content.

* **Improvements**
  * Safer handling when stripping line breaks.
  * More robust string handling in template helpers.
  * Error logs now include filename for better diagnostics.
  * Updated FHIR resource counts.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `be61906cb7e6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.