# Issue

**Title:** Fix dloglik crash when using CG optimizer with warped BLR models

## Description

# Fix `dloglik` crash when using CG optimizer with warped BLR models

## Description

This PR fixes a bug where `BLR.fit()` crashed with a misleading `Unknown function dloglik` error when attempting to use the `cg` optimizer in combination with a warp function (e.g., `warpsinharcsinh`).

The root cause was that analytical gradients (`dloglik`) are not implemented for warped models. When the user manually selected `optimizer="cg"`, `fit()` passed the unsupported `dloglik` function to the SciPy optimizer, which resulted in a hard crash during optimization.

## Changes

- Added a validation check in `BLR.fit()` before optimization begins.
- If `optimizer="cg"` is used with a warped model, `fit()` will:
  - Log a warning indicating that analytical gradients are unsupported.
  - Automatically fall back to the default `l-bfgs-b` optimizer, which correctly uses numerical approximations.
- Added a new structured warning `WARNINGS.BLR_CG_NOT_SUPPORTED_WITH_WARP` in `output.py` for clarity.

## Closes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57bdf51e6603`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.