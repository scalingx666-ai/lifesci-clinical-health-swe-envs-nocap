# Issue

**Title:** [UPDATE] Make Coverity depend on Main branch and use googlegroups email address

## Description

H, 

coverity.yml now makes Coverity depend on **master** branch instead of main. This pr address this. 

It also starts using a googlegroups email distribution list instead of using individual emails of developers.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b5de08f13d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.