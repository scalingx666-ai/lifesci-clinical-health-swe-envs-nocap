# Issue

**Title:** [FIX] Non-regression tests for `center-nifti` catch `time.strftime` only once

## Description

Exports timestamp computing in another function then patches it to avoid catching all underlying instances of `time.strftime`, for example through `cprint`. This was probably introduced when logging level was upgraded to DEBUG in tests 6 months ago.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1377db6aca84`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.