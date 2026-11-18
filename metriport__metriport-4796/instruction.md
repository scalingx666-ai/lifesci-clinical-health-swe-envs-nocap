# Issue

**Title:** ENG-530 Updates for CQ SOAP body

## Description

Part of ENG-530

### Description

- Patient name and address arrays no longer produce invalid <0> tag wrappers

### Testing

- Local
  - [x] Send a request to ourselves and make sure the format is proper
- Staging
  - [x] Test with testing partners
- Production
  - [ ] Try FF with a couple CXs

### Release Plan
- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added response-archiving hooks after successful XCPD requests to improve traceability and troubleshooting.

* **Bug Fixes**
  * Prevents duplicate patient name entries in outbound patient discovery requests by sending a single, consistent name.
  * Simplifies address handling to avoid multiple street lines being emitted unnecessarily, reducing malformed or verbose address data.

* **Refactor**
  * Streamlined envelope construction logic so livingSubjectName is included only when a valid single name is present, ensuring cleaner, more predictable outbound messages.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `97dc6bf50c18`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.