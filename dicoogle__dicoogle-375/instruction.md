# Issue

**Title:** Remove org.eclipse.jetty.jetty-jsp dependency

## Description

It's been a long while since Dicoogle used Java Server Pages. Still, I would advise a bit of testing before merging this one.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8748eac7e071`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.