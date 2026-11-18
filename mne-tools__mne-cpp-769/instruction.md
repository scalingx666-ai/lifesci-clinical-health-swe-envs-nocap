# Issue

**Title:** [FIX] Show file and filter info beneath the data viewer

## Description

Hi, 

There is a problem with the way info is now displayed in the plugin rawdataviewer in mne_analyze. Instead of printing the information of the file and the filter applied in the title bar, we can do it at the bottom in a label bar. 

There is a little bit less space because there are other labels related to the time already printed there, but I think it is fine (at least for now).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `da1dfc6ff609`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.