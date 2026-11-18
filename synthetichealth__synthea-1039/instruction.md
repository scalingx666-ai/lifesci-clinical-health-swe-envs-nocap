# Issue

**Title:** Fix lab value range order of magnitude and unit test units of measure.

## Description

This PR fixes some lab values where the ranges were off by an order of magnitude according to the units of measure.

A unit test is also changed to fix a unit of measure to be valid according to UCUM.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a5c67e046ac9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.