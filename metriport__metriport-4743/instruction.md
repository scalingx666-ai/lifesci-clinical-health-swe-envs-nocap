# Issue

**Title:** ENG-530 Updates to SOAP envelope on CQ XCPD

## Description

Part of ENG-530

### Description

- Slightly changing the structure of the XCPD soap envelope

### Testing
- Staging
  - [x] Check with testing partners
- Production
  - [ ] Monitor in prod

### Release Plan
- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added a feature flag (default off) to toggle a new SOAP envelope format for outbound XCPD (ITI‑55) messages.
  * Exposed utilities to list CXs with the flag and check flag status per CX.

* **Improvements**
  * New envelope uses a URN-wrapped ITI‑55 body with a fuller PRPA_IN201305UV02 payload for improved interoperability.

* **Behavior Changes**
  * Signing/sending flow now evaluates the flag and selects the appropriate envelope shape.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c67300bfe4e8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.