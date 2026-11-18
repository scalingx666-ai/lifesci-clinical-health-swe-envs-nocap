# Issue

**Title:** fix(server): reject external auth callbacks with mismatched iss

## Description

When the identity provider callback includes an RFC 9207 `iss` parameter and the identity provider has a configured issuer, require them to match.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e9200d7f2045`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.