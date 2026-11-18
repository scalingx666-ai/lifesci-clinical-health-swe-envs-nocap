# Issue

**Title:** [FIX] MNE Scan - writing to file calibration values

## Description

- Fix writing to file with wrong values by not accounting for calibration (calling correct write_raw_buffer)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `961f8fa408c5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.