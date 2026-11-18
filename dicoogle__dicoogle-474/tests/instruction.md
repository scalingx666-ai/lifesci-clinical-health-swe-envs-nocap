# Issue

**Title:** Added missing SOPClassUIDs

## Description

Added missing SOPClassUIDs:

- UID.VLWholeSlideMicroscopyImageStorage
- UID.BreastTomosynthesisImageStorage
- UID.XRayRadiationDoseSRStorage

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a7a9ed6f29d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.