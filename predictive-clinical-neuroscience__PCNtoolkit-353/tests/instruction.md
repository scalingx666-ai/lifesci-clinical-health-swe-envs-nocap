# Issue

**Title:** Fix NormData netcdf implementation #345

## Description

I have addressed the issues in the previous PR (#345) related to saving the NormData as a netCDF file. Updated things:

1) Instead of removing and re‑introducing the attributes, I now serialize them with `json.dumps`, so they can be easily saved as a `.nc` file.
2) Added a `has_registered_metadata` method that checks whether the batch‑effect‑related attributes already exist and are not empty. If they do, `register_batch_effects` will not re‑register them. This prevents re‑initialization of batch effects, which could otherwise create discrepancies between the train and test sets during loading.
3) Added a test as recommended.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5cb3e81415a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.