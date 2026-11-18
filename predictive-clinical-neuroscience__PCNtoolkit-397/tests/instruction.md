# Issue

**Title:** Fix :  Silent data corruption in load_centiles due to unassigned pandas sort

## Description

In response to issue #396

I have added a simple fix by making the sorted dataframe actually reflect. This makes the previously ineffective line now effective.
This fix has been verified by me.

This can also be verified by doing the change inside the Colab notebook I gave (it installs an editable version of pcntoolkit). After making the change, please restart the notebook, and the bug should not happen.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3187f8034cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.