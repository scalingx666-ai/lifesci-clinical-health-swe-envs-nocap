# Issue

**Title:** DICOM services - bring patches from 2.5.X releases to main stream

## Description

Bringing two patches to the mainstream:

- Applying the allow to change DICOM C-STORE SCP parameters #446
- Improve logging of C-MOVE SCP to better troubleshoot potential issues. #452

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b6fcac9ea82`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.