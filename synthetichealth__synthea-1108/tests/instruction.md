# Issue

**Title:** Fix template to account for properties with values of false

## Description

The original code just looked for the presence of the alcoholic, homeless and smoker properties but ignored their value, this PR checks that the value is both present and true.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a5228488e462`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.