# Issue

**Title:** Remove duplicate SOP classes in transfer options

## Description

These two SOP classes were appearing twice in the global transfer options list. Likely a mistake from #474.

There could probably be some more cleaning up in this class, but I kept the PR simple to avoid having too many collisions with #516.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `185e875e1ec5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.