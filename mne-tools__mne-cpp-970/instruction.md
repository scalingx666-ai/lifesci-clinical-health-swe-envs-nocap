# Issue

**Title:** [ENH] Flexible choice of cluster size

## Description

Added functionality to allow for a flexible choice of the cluster size of the clustered forward solution. Before the cluster size was hard-coded.

Furthermore fixed a small bug which would lead to crashes due to a segfault:

Deleting the QSharedDataPointer in compute_fwd.cpp causes a segfault when later dereferencing *m_eeg_forward_grad.data()/*m_meg_forward_grad.data() in the call of compute_forward_eeg/compute_forward_meg.

There might be a way to fix this while still deleting the (basically empty) object behind the shared pointer. However, as far as I can see we do not have a guarantee that the value of m_pSettings->compute_grad does not change, so if it would switch to true later on and for some reason calculatedFwd() gets called we would have a problem with the current code anyway.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `32d90957c1d1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.