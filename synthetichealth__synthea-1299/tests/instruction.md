# Issue

**Title:** Fix physiology simulations when running from JAR

## Description

Fix how physiology SBMLs are being loaded to ensure they work when running from JAR. Also cleans up a few things which are now unused.  

Tested on MacOS native and JAR, and Windows native and JAR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9ad8bbb725d3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.