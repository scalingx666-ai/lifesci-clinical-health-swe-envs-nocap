# Issue

**Title:** [FIX] LIB. Problem with static global variable inside the fiff library.

## Description

As mentioned in slack, there might be a problem with the life span of a static global variable in a library. 
This attempts to solve this issue, with a minimum as possible alteration to how the variable is working right now.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4de186c30542`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.