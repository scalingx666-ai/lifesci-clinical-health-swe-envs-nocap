# Issue

**Title:** Add json_begin and json_end Methods For Iterating Over Raw JSON in a Collection

## Description

Add json_begin and json_end Methods For Iterating Over Raw JSON in a Collection

- Add methods json_begin & json_end to the ResourceCollection class to allow
  callers to iterate over the raw JSON of the resources in the collection. This
  is opposed to the begin & end iterators which yield protocol buffer
  representations of the resources.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `89981c64ae0b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.