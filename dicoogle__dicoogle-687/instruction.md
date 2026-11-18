# Issue

**Title:** Fix application of task cleaning hook in RunningIndexTasks

## Description

Pull request #441 was based on Dicoogle 2, but by the time we merged it in Dicoogle 3, we were already using another method overload for `addTask` which evaded our hook that cleans old tasks.

Should fix the situation reported in .

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2fa3510b17e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.