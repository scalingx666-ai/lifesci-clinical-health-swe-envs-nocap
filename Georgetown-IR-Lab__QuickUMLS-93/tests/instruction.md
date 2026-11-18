# Issue

**Title:** fix import error: cannot import name 'MEDSPACY_DEFAULT_SPAN_GROUP_NAME'

## Description

Bug:
Concurrent installation of medspacy and quickumls results in:
ImportError: cannot import name 'MEDSPACY_DEFAULT_SPAN_GROUP_NAME' from 'quickumls.constants'
when trying to run the first cell of 11a quickumls medspacy notebook.
Comparison with medspacy installation without quickumls installation revealed additional line on constants.py.

Fix:
add MEDSPACY_DEFAULT_SPAN_GROUP_NAME in constants.py

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a3ba0b3559da`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.