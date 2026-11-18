# Issue

**Title:** fix posthog api not working on webhook sender

## Description

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1100

### Dependencies
None

### Description
Fix posthog not getting any analytics from webhook sender

### Testing

See image (This is in staging)

<img width="428" height="208" alt="Screenshot 2025-09-29 at 12 26 21 PM" src="https://github.com/user-attachments/assets/433c3d7f-8ed7-4687-8236-60d42c443cd2" />


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- New Features
  - None.
- Refactor
  - Analytics events are now sent only after securely retrieving the API key, preventing unguarded analytics calls.
- Chores
  - Configured analytics API key to be retrieved from secret management and provided to the service via environment variables.
- Style
  - Minor formatting cleanup with no functional impact.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4ffecb0bc084`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.