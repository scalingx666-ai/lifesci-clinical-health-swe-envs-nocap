# Issue

**Title:** [ENH] MNEAnalyze saves last folder where data were loaded from

## Description

A little bit of refactoring in the way in which the QSettings was used by mainwindow to store the dark theme and a few other info.
Also, a few warnings addressed, not solved. but at least, not showing without any chance of actually breaking the code. 
And finally, added a much needed feature of storing the directory from where the last fif file was loaded.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `14693cbff3b6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.