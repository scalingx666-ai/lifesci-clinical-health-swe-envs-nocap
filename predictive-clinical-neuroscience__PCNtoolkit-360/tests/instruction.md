# Issue

**Title:** fix: add NotImplementedError to incomplete from_fsl and from_bids met.

## Description

**Description**

 

As discussed in the linked issue, the `NormData.from_bids` and `NormData.from_fsl` methods were incomplete. `from_bids` was empty, and `from_fsl` did not return the constructed object, leading to silent failures when users attempted to use them.

**Changes Made**
* Updated `from_bids` to raise `NotImplementedError("BIDS loading is not yet implemented in NormData.")`.
* Updated `from_fsl` to raise `NotImplementedError("FSL loading is not yet implemented in NormData.")`.

**Testing**
* I have verified that calling these methods now raises the appropriate error message instead of returning `None`.
* Ran existing tests using `pytest test/test_dataio/test_normdata.py` to ensure no regressions were introduced.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4a9d8a9dadd5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.