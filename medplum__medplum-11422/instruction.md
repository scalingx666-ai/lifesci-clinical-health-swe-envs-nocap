# Issue

**Title:** fix(server): apply login and MFA rate limits regardless of path case …

## Description

Express routes paths regardless of case and with one trailing slash, but
rate-limit categories compared exact strings. Requests like /AUTH/LOGIN,
/auth/login/ or /API/Projects/{id}/Auth/Login reached the login and MFA
handlers under the much higher default limit.

Lowercase the path and strip one trailing slash before choosing a
category. Each category now lists its paths, prefixes and excluded
paths as data instead of using a match function, and a test checks
that they are all lowercase.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cc94a65b2e48`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.