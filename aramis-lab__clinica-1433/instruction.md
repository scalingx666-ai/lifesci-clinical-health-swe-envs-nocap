# Issue

**Title:** [ENH] In `center-nifti`, give the option to the user to choose the centering threshold

## Description

following #1418 

Changes the option of `--center_all_files` to `--threshold` above which images are to be centered.

In other PR : 
- Add non regression tests that checks inside images and txt file
- Change CI data if necessary (might be interesting to have different thresholds/modalities to test)
- Use the new NiftiImage class in `_get_world_coordinate_of_center`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57cbde74d6b2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.