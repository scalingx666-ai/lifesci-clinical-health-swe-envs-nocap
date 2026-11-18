# Issue

**Title:** In this stage of the installation $CURDIR/bin does not exist.

## Description

A fresh installation crashes here, because the $CURDIR/bin directory is being created by the virtualenv command.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `050c6697602a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.