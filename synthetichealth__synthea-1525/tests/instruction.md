# Issue

**Title:** Flexporter updates - October 2024

## Description

A few new features for the flexporter:

1. A new `if` field that can be used in `create_resource` to conditionally set a field. The use case that inspired this is shown in the unit test - creating ServiceRequest based on Procedure, setting ServiceRequest.authoredOn = Procedure.performed, but Procedure.performed is either a dateTime (ie, primitive) or a Period (ie, an object) so the types need different handling. Previously the only way to do this was with two separate actions with different applicability.
2. Allow deleting resources by FHIRPath instead of just by resource type. The use case that inspired this is deleting some of the SDOH conditions to clean up a record for a demo
3. Allow functions to be nested within definitions. Previously a function call such as `getAttribute` could only be used as the top-level `value`, now `value` can be a map and one of the sub-values can be the function.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9de046068059`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.