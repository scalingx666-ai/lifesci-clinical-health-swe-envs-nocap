# Issue

**Title:** [FIX] MNE_Analyze store right-click context menu in fiffrawview plugin as member variables.

## Description

Instead of allocating a new menu and action each time the right-click mouse button is pressed, we store and reuse.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `11f9db56a626`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.