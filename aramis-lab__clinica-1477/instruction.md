# Issue

**Title:** [REF][TEST] Refactor and test `_select_sessions` in UKB-to-BIDS utils

## Description

While working on UKB-to-BIDS to extend #1450, I dug into the code for `sessions.tsv` writing and noticed a function that could be both improved and tested : 


https://github.com/aramis-lab/clinica/blob/c9ab28bec76c10ba8f8866555b39d713f640ce5a/clinica/converters/ukb_to_bids/_utils.py#L415-L453


The way of testing for nans was modified since it was doing nothing as it was.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c9ab28bec76c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.