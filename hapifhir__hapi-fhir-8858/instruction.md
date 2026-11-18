# Issue

**Title:** Support operation parameters in body when delete is enabled

## Description

An inappropriate check in the $operation method parameter assembler meant that parameters for an $operation method supplied in a request body (i.e. using a `Parameters` resource) were ignored if the method supports the delete verb.

This meant (for example) that the `$export-poll-status` failed to fetch parameters from the request body.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd4b5fc2457b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.