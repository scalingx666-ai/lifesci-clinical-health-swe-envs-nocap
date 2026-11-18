# Issue

**Title:** ENG-1225: Improve regex for finding unescaped ampersands

## Description

Issues:

- https://linear.app/metriport/issue/ENG-1225

### Dependencies

- Upstream: None
- Downstream: None

### Description

The current normalization is insufficient for finding all cases where there is an unescaped ampersand, since an incorrectly escaped ampersand may be next to non-space characters. This PR is in response to a large number of on-call errors related to this issue - see the ticket for more details.

### Testing

- Local
  - [x] ran `cda-to-html.ts` in `utils` with the failing XML, works correctly with better normalization
  - [x] run the FHIR integration test on 10k files
- Staging
  - [ ] check normal CDA to visualization is working
- Production
  - [ ] ensure normal CDA to visualization works

### Screenshots
<img width="390" height="327" alt="Screenshot 2025-10-07 at 2 27 53 PM" src="https://github.com/user-attachments/assets/85dda468-e7ce-41e0-96db-3611b592adf3" />


### Release Plan

- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * CLI added for cda-to-html; payload cleanup now runs during CDA-to-HTML and CDA-to-PDF/visualization conversions.
* **Bug Fixes**
  * Improved ampersand escaping to prevent broken HTML/entities while preserving existing escapes and common XML entities.
* **Chores**
  * Centralized document cleanup across conversion flows; runtime updated to use compiled output with a mandatory build step.
* **Tests**
  * Added comprehensive tests covering ampersand escaping and edge cases.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `931345717f80`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.