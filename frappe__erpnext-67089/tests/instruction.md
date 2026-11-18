# Issue

**Title:** fix(manufacturing): check Routing read permission in BOM get_routing (backport #65955)

## Description

Backport of #65955 to `version-16-hotfix`.

The BOM method `get_routing` copied the operations of the selected Routing into the BOM without checking that the user can read that Routing. It now checks read permission on the Routing first.

**Fix:** `get_routing` checks read permission on the Routing and then calls the new `set_operations_from_routing`, which holds the old body. The BOM save path (`set_routing_operations`) calls `set_operations_from_routing` directly, so saving a BOM works as before. ()

**Changes compared with develop:** On this branch `get_routing` builds the field list inline (develop has `_get_routing_fields`). The old body moves without changes into `set_operations_from_routing`; the develop refactor is not brought in. #67084 also changes `bom.py` and `test_bom.py` in other places. Each merges on its own.

 for the example and the steps to test.

### Tests

- `test_get_routing_checks_routing_read_permission`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_bom.py` (complete file): 71 pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.