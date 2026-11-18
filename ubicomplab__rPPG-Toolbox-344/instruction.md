# Issue

**Title:** fix SNR calculation error

## Description

According to [scipy.signal.periodogram](https://docs.scipy.org/doc/scipy-1.5.2/reference/generated/scipy.signal.periodogram.html#scipy.signal.periodogram),the signal spectrum that scipy.signal.periodogram returned is represented as a power spectrum, so there is no need for additional power calculations.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c0604b5a5f7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.