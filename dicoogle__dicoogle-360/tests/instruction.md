# Issue

**Title:** Validate UUID provided to /exportFile

## Description

This checks whether the identifier to the exported CSV file is actually a UUID. It fixes a vulnerability on Windows systems which would allow a user to retrieve an arbitrary file from the server.

I took the liberty of adapting this endpoint to our JSON error output (#193), and ensuring that the content-type is JSON when sending an error with our utility function.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4fb84097e51`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.