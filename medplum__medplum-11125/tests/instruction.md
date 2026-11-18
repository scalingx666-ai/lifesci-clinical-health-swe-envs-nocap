# Issue

**Title:** apply ActivityDefinition dynamic values to a copy of the ServiceRequest draft

## Description

ActivityDefinition dynamicValue expressions are now applied to a copy of the draft ServiceRequest, and values returned by an expression are copied before being written.

The Task created for a ServiceRequest now takes its requester from the ServiceRequest so the two always agree.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `68c347e745a2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.