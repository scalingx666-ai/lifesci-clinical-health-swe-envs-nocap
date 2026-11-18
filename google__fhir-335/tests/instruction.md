# Issue

**Title:** Modifies proto generation to use TerminologyExpander to generate code and value set enums.  Regenerates r5 SearchParameter, OperationDefinition, and GraphDefinitions to use this expander, which correctly handles the "All Resources from all versions" valueset.

## Description

Modifies proto generation to use TerminologyExpander to generate code and value set enums.  Regenerates r5 SearchParameter, OperationDefinition, and GraphDefinitions to use this expander, which correctly handles the "All Resources from all versions" valueset.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65c71f5ba043`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.