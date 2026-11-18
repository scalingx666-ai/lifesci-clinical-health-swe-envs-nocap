# Issue

**Title:** Consider all parameters in server storage service

## Description

Adding new storage destinations via the web API was slightly faulty. Due to a possible regression in the change of server settings format, it was ignoring the `description` and `public` properties. This PR brings these properties back and adds more input validation.

- Bring back `public` and `description`  as parameters for adding a storage destination
- Validate `port` as a TCP port
- Validate `type` to be either add or remove

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5507ee7d8b8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.