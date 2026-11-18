# Issue

**Title:** Fix issues with NPEs related to the employment module

## Description

The simulation expects every person to have an employment model set in their attributes. If a person was generated an a county where the `sdoh.csv` file did not have a row, the employment model would not get set. This change uses the state average information when the desired county can not be found.

This PR addresses Pattern 2 as described in #1380.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6192ed703d85`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.