# Issue

**Title:** fix: refresh the Result editor when switching Observations

## Description

Issue description
When opening another Observation, the Result editor could show text from the previous record. Refreshing the page showed the correct saved Result.

Fix applied
Replaced the Result control through Frappe’s layout.replace_field method, so Frappe tracks and refreshes the visible editor for the current Observation. Result Interpretation is unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7bb34f56a417`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.