# Issue

**Title:** [TEST] Change function tested in non-regression for center-nifti

## Description

#1438 follow-up

- Change from center_all_niftis to center_nifti
- Add non regression tests on the txt file

As of now breaks the CI because the txt file was not added to the CI ref folder. I would need to update the CI with it if this PR is validated. The test that is done on the file structure should stay as is though (i.e. not taking into account the txt file) since there is a timestamp in the txt file name.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `31b2838ecc2f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.