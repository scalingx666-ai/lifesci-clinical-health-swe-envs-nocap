# Issue

**Title:** [MAINT] Add 'fits per second' control to hpi.

## Description

Preamble:
This is not a permanent fix by any means, this is a quick fix to have the continuous hpi in its current state more easily debugable during runtime (with different setups). This is a control for making iNumberOfFitsPerSecond variable during runtime, which was found to be a temporary solution to getting the continuous hpi fitting working on different incoming frequencies and data chunk sizes. iNumberOfFitsPerSecond does not set the number of fits per second, it is used to set the sample window used to perform the continuous fit, but the fit still seems to occur at whatever rate the data comes in. Treat this as a tuning variable, find a setting that works and leave it there. With that being said:

- Add controls for setting fits per seocnd in HpiSettingsView
- Make iNumberOfFitsPerSecond changeable during runtime

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `505f292a20f9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.