# Issue

**Title:** [REF] Adapt Stat Volume to SPM25

## Description

This PR modifies a bit the code in the `stat-volume` pipeline to allow for SPM25 standalone usage. 

What has been done :

- Remove parts that were used by the set-up MATLAB + SPM
- Adapt the .m templates for SPM Standalone
- Correct unit tests
- Use SPM standalone set-up in non-regression tests
- Tested on both macOS and Linux (CI)

Follow up :

- Verify the Non-regression tests validate when merged

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9746c988d712`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.