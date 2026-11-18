# Issue

**Title:** Add explicit real part extraction when filtering BVP in ICA_POH

## Description

Pretty simple change to just explicitly extract the real part before casting. This change prevents the following warning message from appearing:

`/playpen/akshay/rPPG-Toolbox/unsupervised_methods/met
hods/ICA_POH.py:44: ComplexWarning: Casting complex values to real discards the imaginary part
  BVP_F = signal.filtfilt(B, A, BVP_I.astype(np.double))`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c7e9fe20fa2b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.