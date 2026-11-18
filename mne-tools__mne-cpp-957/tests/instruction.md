# Issue

**Title:** Fix colors on Linux

## Description

Add correct echo flag `-e` on linux systems to escape special characters properly. (Tested on CentOS)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `72d952bcba63`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.