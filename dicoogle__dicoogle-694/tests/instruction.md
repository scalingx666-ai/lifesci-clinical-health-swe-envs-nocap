# Issue

**Title:** Add robustness to DIMGeneric against BodyPartThickness

## Description

This fixes a situation found in the wild, where the matching of certain search results via C-FIND would lead to a server error.

### Summary

At `DIMGeneric#fillDim`, do not assume that `BodyPartThickness` is a string, because some index sources might save it as a double.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `71e1d82c82d7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.