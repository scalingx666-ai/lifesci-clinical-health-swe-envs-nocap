# Issue

**Title:** Unemployment enhancements

## Description

This PR contains fixes for the SDoH HRSN submodule as well as a new model of unemployment.

Previously, people in Synthea would be selected to be unemployed for their whole life in the simulation.

With this change, people will have a chance to become unemployed based on the unemployment rate for their county. Unemployment status is checked every 6 months.

This addresses #1272

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e624912abcaf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.