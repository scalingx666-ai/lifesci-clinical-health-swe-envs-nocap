# Issue

**Title:** New file list feature

## Description

Added FILE_LIST_PATH feature. Generated file list that is used to load data from preprocessed datasets. Set default value of FILE_LIST_PATH to CACHED_PATH + `/DataFileLists/`.
Users can still edit FILE_LIST_PATH in config yaml files if they so choose. 

All code was tested on PURE_PURE_UBFC_TSCAN_BASIC

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d364de4ad875`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.