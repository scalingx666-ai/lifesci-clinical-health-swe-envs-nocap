# Issue

**Title:** fix(server): reset user security state on email change

## Description

A couple behavior changes worth calling out:

`$update-email` and SCIM changes sign the user out of all sessions in addition to canceling open links

SCIM email changes clear `emailVerified`; SSO users get it back on their next login but password users stay unverified so we may want to revisit this decision.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `14ad9501016d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.