# Issue

**Title:** Fix comparison with NAN in heatmap.py

## Description

#### Background
This PR , where the use of `np.NAN` in `heatmap.py` causes an `AttributeError` in NumPy version 2.1. To resolve this, all instances of `np.NAN` are replaced with `np.nan`, ensuring compatibility with both current and future versions of NumPy, as recommended by the [NumPy stable documentation](https://numpy.org/doc/stable/reference/constants.html#numpy.nan) and the [NumPy 1.26 documentation](https://numpy.org/doc/1.26/reference/constants.html#numpy.NAN).

#### Current Behavior
Using `np.NAN` results in `AttributeError: module 'numpy' has no attribute 'NAN'`, causing errors in NumPy 2.1.

#### Expected Behavior
The code will now use `np.nan` for NaN handling, eliminating the `AttributeError` and ensuring compatibility across NumPy versions.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2864cc9c69f4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.