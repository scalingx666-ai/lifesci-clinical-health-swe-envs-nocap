# Issue

**Title:** Provide full search results on result-batch plugin mount event

## Description

The webapp does not provide the full search results on the `result-selection-ready` event.

This PR fixes this issue by providing both the search results and the search results that were selected via the UI, instead of only providing the selected entries.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6e0623335af1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.