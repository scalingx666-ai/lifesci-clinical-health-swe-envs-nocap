# Issue

**Title:** [FIX]  MNEAnonymize Use QDate instead of QDateTime when reffering to birthday date.

## Description

In fiff files, birthday date is coded in julian calendar (with an integer number).  It is just a date, not a date and time. Thus, I change here the use of QDateTime for the use of QDate for a more correct use. 

I also got to change the use of const references more to gain a bit of simplicity/efficiency. 

Let's see what I break.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d43640856487`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.