# Issue

**Title:** fix(warp): add input validation to WarpLog for non-positive values

## Description

## Summary
 
As discussed in issue #365.

Add input validation to `WarpLog.f()` to prevent silent `NaN` failures when input data contains zero or negative values.
Added input validation in `WarpLog.f()` that raises a clear `ValueError` when non-positive values are detected:
```python
if np.any(x <= 0):
    raise ValueError(
        "WarpLog requires all input values to be strictly positive (> 0). "
        "Your data contains zero or negative values. Consider:\n"
        "  1. Using WarpBoxCox or WarpSinhArcsinh which handle negative values\n"
        "  2. Setting outscaler=None if using WarpLog (warp is applied after scaling)"
    )
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13e979c05818`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.