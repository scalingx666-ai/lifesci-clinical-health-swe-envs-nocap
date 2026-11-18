# Issue

**Title:** [FIX] MNE Anonymize

## Description

Couple of things in the app needed to get fixed. 

 - Use of console only in debug mode. 
 - delete a qdebug printing the date that got leaked into production version. 
 - rewrite QMAKE_TARGET_DESCRIPTION variable so that windows task manager correctly prints the application name.
 - fix a warning regarding a const qualifier in a signal.
 - dont emit in constructors

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5f86d1070e9f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.