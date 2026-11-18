# Issue

**Title:** [REF] Proposition for AIBL Json creation

## Description

This PR proposes a solution to write the json file associated to a PET image for the AIBL dataset using the header of the dicom image. 

Discussion (for later):
-  can this be used for other than AIBL ?
- would using a class be beneficial ? I am starting to get a lot of : if modality do something

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f907bc5f4f7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.