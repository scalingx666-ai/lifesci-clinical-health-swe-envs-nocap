# Issue

**Title:** fixed spacy language map issue

## Description

Spacy updated d its language map so that it doesnt work with the shortened language names. I fixed this so the lang_map now works with spacy > 3

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0b5db059fbe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.