# Issue

**Title:** [REF] Refactor function `clip_img`

## Description

Follow-up PR of #1355 

This PR proposes to:

- Add a new `clip_nifti` function to `clinica.utils.image` for generic clipping of nifty images
- Refactor `clip_img` to use `clip_nifti` with the computed threshold
- Provide the pipeline base directory as the `output_dir` of the clipping task such that clipped images aren't written in the current folder.
- Add unit tests for function `clip_nifti` and `clip_img`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ab080992bba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.