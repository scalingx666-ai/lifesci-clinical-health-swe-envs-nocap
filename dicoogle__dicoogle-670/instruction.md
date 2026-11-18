# Issue

**Title:** Update Bcrypt dependency and password hash service

## Description

### Summary

- Update bcrypt and password hashing
   - bcrypt 0.10.2
   - Make password hashing strength configurable via JVM variable (default stays at 10)
- Fix `HashService` for very large passwords
   - Set BCrypt version to 2B
   - Apply existing long password strategy in verification
   - Add `HashServiceTest`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0a514aac7115`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.