# Issue

**Title:** [Dicoogle2] Fix DICOM Storage flipped priority by AE title

## Description

- invert order for priority AE title
   - its presence should represent a HIGHER priority rather than a lower one
- move priority implementation to static method so it does not depend on a storage service instance
- add test prove that this bug was fixed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `49c1982779b1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.