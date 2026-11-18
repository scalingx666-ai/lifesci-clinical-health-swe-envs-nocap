# Issue

**Title:** fix: guard dloglik for heteroskedastic models and fix alpha iteration

## Description

### Changes

- **Guard in `fit()`**: Auto-switch from `cg` to `l-bfgs-b` when `heteroskedastic=True`, since `dloglik` doesn't support heteroskedastic gradients
- **Guard in `dloglik()`**: Raise `NotImplementedError` for heteroskedastic models (consistent with existing warp guard)
- **Fix Loop 2 in `dloglik()`**: Iterate over `alpha` instead of `beta` for scaling parameter derivatives
- **Add test**: CG + ARD (non-heteroskedastic) fits successfully

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e72ae91f0320`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.