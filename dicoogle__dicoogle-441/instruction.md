# Issue

**Title:** Fix memory leak in the completed/failed indexing task.

## Description

This PR avoids to keep all indexing tasks in memory.
The oldest not running tasks are cleaned, to guarantee a hooked memory cleaning process. 

Base is master, but planned to merge in dev as well.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9104bbc916cb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.