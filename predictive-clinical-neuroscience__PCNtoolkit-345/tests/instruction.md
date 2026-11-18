# Issue

**Title:** Additional functionality and improvements in the NormData class.

## Description

- Added functions to save and load the NormData class in NetCDF format (i.e., .nc file). This method is significantly more efficient and faster than saving as a .csv file, particularly for large datasets.
- Implemented the TODO for the "register_batch_effects" function, which now utilizes vectorized operations to improve performance.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5cb3e81415a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.