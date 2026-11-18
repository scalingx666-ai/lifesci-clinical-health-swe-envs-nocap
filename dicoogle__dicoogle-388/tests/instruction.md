# Issue

**Title:** Revamp user file handling and cryptographic code

## Description

I believe it fully .


- Replace all uses of the SHA-1 algorithm with BCrypt, a more suitable password hashing algorithm. It's still worth noting that this codebase was using SHA-1 far before the SHAttered attack was known.
- Make user file encryption actually work. This will happen by default unless a users file already exists without the respective key file.
- Try to set owner read-only permissions to users encryption key
- Refactor code around the `Cipher` API. I'm still not quite convinced that `Cipher` was being misused, though.
- Change user credentials file name to just "users" (since it might be encrypted, the .xml extension is misleading)

This is another breaking change for Dicoogle, each new deployment will have to create user credentials again.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `47ab61432fb5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.