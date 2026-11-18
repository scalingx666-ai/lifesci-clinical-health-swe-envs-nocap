# Issue

**Title:** Add encrypt-users-file to server settings

## Description

This was overlooked when creating the new server settings format, but with the recommendation to not implement server settings readers, we can safely add new properties without calling it a breaking change.

- [sdk] add getter and setter for property to encrypt the users file (`EncryptUsersFile` in legacy)
- [core] implement new methods in server settings impl
- update tests to ensure it is loaded and migrated from legacy
- Use `encrypt-users-file` setting in UserFileHandle
   - do not try to encrypt anything if false
   - update comments to reflect the current behavior

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ff92c3b1cd6e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.