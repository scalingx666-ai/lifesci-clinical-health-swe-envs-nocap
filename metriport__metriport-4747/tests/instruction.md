# Issue

**Title:** RELEASE CQ SOAP Env update + CW patient management improvement

## Description

Issues:

- https://linear.app/metriport/issue/ENG-530
- https://linear.app/metriport/issue/ENG-1164

### Description

- 
- 

### Testing

Check each PR.

### Release Plan

- :warning: Points to `master`
- [ ] Merge this
- [ ] FFs have been set in Staging, Production, and Sandbox

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- New Features
  - Per-customer feature flag to enable a new SOAP envelope for outbound patient discovery (XCPD), allowing controlled rollout.
  - Alternative SOAP body generation path when the flag is enabled.

- Improvements
  - More reliable patient linking with retries, robust error handling, and validation, resulting in more accurate links and fewer failures.
  - Automatic upgrade of probable links when validated.

- Refactor
  - Consolidated CommonWell v2 patient linking into a dedicated module, simplifying patient workflows and reducing complexity in related components.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `53466487b323`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.