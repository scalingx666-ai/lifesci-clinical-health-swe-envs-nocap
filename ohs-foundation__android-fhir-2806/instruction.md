# Issue

**Title:** Upgrade all self-hosted ubuntu-22.04 runners to ubuntu-24.04.

## Description

This is a http://go/LSC run by http://go/ghss to upgrade all self-hosted ubuntu-22.04 runners to ubuntu-24.04.

This is a courtesy PR to help you upgrade to the latest release of ubuntu runners, it is not mandatory at this time.

WARNING: We do not know if the updated label is compatiable with your workflow or not.

If you do not want to merge this PR, feel free to close it.

More context and feedback: http://b/406537467

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e1e3027ca2b4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.