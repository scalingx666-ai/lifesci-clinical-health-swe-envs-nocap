# Issue

**Title:** Alternative RMSE SE fix to deal with abnormal distirbutions of errors

## Description

Different, albeit similar in intention, approach that better deals with abnormal distributions of errors and should be more intuitive. This is in contrast to the previous approach using the delta method that was less intuitive because it did not directly measure the variability of errors in their native squared form.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2add21e1e19d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.