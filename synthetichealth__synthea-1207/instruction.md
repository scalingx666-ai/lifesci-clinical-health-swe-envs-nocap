# Issue

**Title:** Fix log4j Error in uberJar

## Description

Switch current uberJar method to use shadowJar plug-in instead of manual assembly

.

Retains the `uberJar` task (just calls shadowJar) but that could be dropped if we edit the GitHub actions file to use the `shadowJar` task instead.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `569e156c6a36`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.