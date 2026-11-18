# Issue

**Title:** Add support for confidential clients

## Description

This adds support for confidential apps as described in http://docs.smarthealthit.org/authorization/#app-exchanges-authorization-code-for-access-token.

I'm sorry about all the extra whitespace changes, my vim is set to automatically delete trailing whitespace on save. If this is an issue, I can figure out how to put them all back.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4aa584b03a69`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.