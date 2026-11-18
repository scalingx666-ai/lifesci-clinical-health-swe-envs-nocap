# Issue

**Title:** fix - bump nutpie to the latest version + add testing action

## Description

Fixes this bug that appears when running fit_predict():

```RuntimeError: Coordinate batch_effect_dims value has unsupported type

Caused by:
    RuntimeError: Could not convert to Value. Unsupported type: ArrowStringArray```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `68c171f32e4b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.