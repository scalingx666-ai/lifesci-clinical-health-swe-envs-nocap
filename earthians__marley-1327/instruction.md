# Issue

**Title:** fix: refresh the Result editor when switching Observations (backport #1317)

## Description

Issue description
When opening another Observation, the Result editor could show text from the previous record. Refreshing the page showed the correct saved Result.

Fix applied
Replaced the Result control through Frappe’s layout.replace_field method, so Frappe tracks and refreshes the visible editor for the current Observation. Result Interpretation is unchanged.<hr>This is an automatic backport of pull request #1317 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f1e8308cd9d9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.