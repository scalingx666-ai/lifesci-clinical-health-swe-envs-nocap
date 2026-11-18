# Issue

**Title:** [ENH] Use newer codecov client, set threshold of 1% decrease coverage, report with colors starting at 1% coverage

## Description

This change helps stabilize the unexpected coverage changes we've been observing in codecov. We disable the check for coverage changes that takes into account only the lines modified in a single pr. We keep using the check that checks for coverage at the complete repo.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bd31738cf675`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.