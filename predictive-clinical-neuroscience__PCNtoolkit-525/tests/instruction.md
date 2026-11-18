# Issue

**Title:** Restructure correlation matrix architecture

## Description

**Notes**

- `CorrelationMatrix.save` not implemented yet. We need to decide in which format we will save. Currently johanna uses pickle but other options are .nc and json (a bit bigger file but easier to read)
- Currently, Johanna does not store the response variable name in the correlation matrix, only in the file path. We should discuss whether to standardise this and then add a check in the code that the response variable in the correlation matrix exists in the normative model.
- `CorrelationMatrix.compute` computes in one object the correlation matrices for all response variables. Johanna computes for **each** response variable one correlation matrix. Should `compute `do the same thing?
- `CorrelationMatrix.load` is written specifically to load the matrices that Johanna saved in `R:\3022017.06\projects\lifespan_hbr\johbay\Velocity\Velocity_models\DES_demented`
- Warn that there is extrapolation when the thriveline covariate range falls outside the range where correlations of the correlation matrix were actually estimated (score() already does this). 

**Tests**
I did not add any tests yet

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f71238e51ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.