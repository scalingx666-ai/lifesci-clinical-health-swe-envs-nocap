# Issue

**Title:** CSV sort patient expenses and payer transitions by time.

## Description

This PR sorts patient expenses and payer transitions by start time.

This helps comprehension of the CSV output when browsing, and also aids in the interpretation of `diff` when comparing multiple runs (e.g., ).

The sortation is per patient, so a `diff` may continue to show discrepancies if `generate.thread_pool_size` is not restricted to `1`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2512c10a5dd4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.