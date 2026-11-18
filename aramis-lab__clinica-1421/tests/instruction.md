# Issue

**Title:** [ENH][TEST] Move logic for file checking and add tests in center_nifti

## Description

In this PR : 
- All the logic for file checking is moved in the private function for centering files
- Unit tests are added
- File overwriting was renewed :
   - Before : it copied only files at the root level (ex : description json) but not nifti files nested in folders if both directories had folders with same names. That is a bit misleading because it looks like it will preserve what is inside the BIDS input and actually... does not.
   - Now : will completely remove files inside the output folder.
   **→ This is a bit radical and could be changed for a solution that iteratively checks files from both folders in a follow-up PR**

In another PR : non-regressions tests should look inside nifti files and check option for overwriting

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d08c0e7f0fe9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.