# Issue

**Title:** PATCH-RELEASE Move incoming s3 upload earlier in the function

## Description

Part of ENG-1168

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1168

### Dependencies
None

### Description
Move incoming s3 upload in mllp server earlier in the function. To not lose data.

### Testing
- Local
  - [x] Send a mllp message with an unsupported trigger event and make sure it uploads to incoming.
  

<img width="948" height="111" alt="Screenshot 2025-09-26 at 1 51 40 PM" src="https://github.com/user-attachments/assets/9f0a2e6c-6d7f-40bd-a2b9-4cef069dcb43" />

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Improved reliability of HL7 notification processing, ensuring unsupported events are handled safely.
  * Standardized file naming for downstream systems.

* **Refactor**
  * Streamlined processing order to enhance stability and observability without changing user-facing behavior.

* **Chores**
  * Enhanced analytics and logging around HL7 notifications for better monitoring and troubleshooting.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `adac8d9ba9ee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.