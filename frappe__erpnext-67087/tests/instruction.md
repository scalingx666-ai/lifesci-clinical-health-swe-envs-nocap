# Issue

**Title:** fix(manufacturing): limit the number of parts read from a STEP design file (backport #65966)

## Description

Backport of #65966 to `version-16-hotfix`.

The STEP reader of BOM Creator expands every path through the assembly structure into its own part row. When subassemblies are shared between several parents, a small file can expand into hundreds of thousands of parts, and the save then runs until the worker times out or runs out of memory. The reader now stops with a clear message when the file has more than 5000 parts.

**Fix:** `StepProductStructure.get_node` counts the parts it builds and throws when the count passes `MAX_PARTS` (5000). ()

**Changes compared with develop:** None. The commit applies without changes.

 for the example and the steps to test.

### Tests

- `test_step_file_with_more_parts_than_the_limit_is_rejected`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_step_file_with_shared_subassemblies_stops_at_the_part_limit`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_bom_creator.py` (complete file): 85 pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.