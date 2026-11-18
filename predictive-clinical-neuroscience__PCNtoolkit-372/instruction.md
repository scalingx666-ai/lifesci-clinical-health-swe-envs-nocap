# Issue

**Title:** enh - add  Y transformation keyword argument in NormativeModel to enforce positivity

## Description

If Y<-1 then log(Y+1) cant be computed (ValueError) but I expect Y to always be >=-1 (since the functionality i added in this pr is only for data that are always positive). If we want to be conservative we can add though a check like:
```
# Validate that values are > -1 (required for log1p)
min_val = float(np.min(data[var].values))
if min_val <= -1.0:
    raise ValueError(
        f"y_transform='log1p' requires all {var} values > -1 but your {var} are not"
    )
```

We can still consider to add a test and/or an example.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `94a26fc311b7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.