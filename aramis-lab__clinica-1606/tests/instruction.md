# Issue

**Title:** [ENH] Adaptation of user id retrieval for docker processes

## Description

When writing the `dataset_description` file for CAPS, the user name of the person who does the processing is retrieved based on uid.  Inside a docker container, you have a uid/gid but that is not associated to a specific user. In other words, you run as a no-name user. As such, this part of the code was not adapted to running with docker and was adapted a little.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd390459b62b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.